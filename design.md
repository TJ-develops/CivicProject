# Design Specification: Public Information Portal with AI Assistant

**Project Name:** Civic Information Portal (Working Title)  
**Version:** 1.0  
**Date:** February 2026  

---

## Table of Contents

1. [System Design Overview](#1-system-design-overview)
2. [User Interface Design](#2-user-interface-design)
3. [Database Design](#3-database-design)
4. [API Design](#4-api-design)
5. [AI Assistant Design](#5-ai-assistant-design)
6. [Security Design](#6-security-design)
7. [Deployment Design](#7-deployment-design)

---

## 1. System Design Overview

### 1.1 Architecture Pattern

**Pattern:** Microservices Architecture with Event-Driven Components

**Rationale:**
- Core website can function independently of AI service
- Each component can scale independently
- Technology flexibility (Node.js for web, Python for AI)
- Easier to maintain and update

### 1.2 High-Level Component Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                             │
│                                                                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │ Web Browser  │  │ Mobile App   │  │ Voice (Phone)│          │
│  │ (Next.js)    │  │ (React       │  │ (IVR)        │          │
│  │              │  │  Native)     │  │              │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                      EDGE LAYER                                  │
│                                                                   │
│  ┌────────────────────────────────────────────────────┐         │
│  │  CDN (CloudFront / Cloud CDN)                      │         │
│  │  - Static assets (images, CSS, JS)                 │         │
│  │  - Cached HTML pages                               │         │
│  │  - Edge caching for API responses                  │         │
│  └────────────────────────────────────────────────────┘         │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                    API GATEWAY LAYER                             │
│                                                                   │
│  ┌────────────────────────────────────────────────────┐         │
│  │  API Gateway (AWS ALB / GCP Load Balancer)         │         │
│  │  - Rate limiting                                    │         │
│  │  - Authentication                                   │         │
│  │  - Request routing                                  │         │
│  │  - SSL termination                                  │         │
│  └────────────────────────────────────────────────────┘         │
└─────────────────────────────────────────────────────────────────┘
                              ↓
        ┌─────────────────────┴─────────────────────┐
        ↓                                           ↓
┌──────────────────────┐                ┌──────────────────────┐
│  WEB APPLICATION     │                │  AI ASSISTANT        │
│  SERVICE             │                │  SERVICE             │
│                      │                │                      │
│  Technology:         │                │  Technology:         │
│  - Next.js 14        │                │  - Python 3.11       │
│  - Node.js 20        │                │  - FastAPI           │
│  - TypeScript        │                │  - LangChain         │
│                      │                │  - Claude/GPT-4      │
│  Features:           │                │                      │
│  - SSR pages         │                │  Features:           │
│  - Search            │                │  - Speech-to-Text    │
│  - Multi-language    │                │  - NLP processing    │
│  - Office locator    │                │  - Eligibility match │
│                      │                │  - Text-to-Speech    │
└──────────────────────┘                └──────────────────────┘
        ↓                                           ↓
┌─────────────────────────────────────────────────────────────────┐
│                      DATA LAYER                                  │
│                                                                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │ PostgreSQL   │  │ Redis Cache  │  │ Vector DB    │          │
│  │              │  │              │  │ (Pinecone)   │          │
│  │ - Schemes    │  │ - Sessions   │  │              │          │
│  │ - Offices    │  │ - User state │  │ - Embeddings │          │
│  │ - Analytics  │  │ - API cache  │  │ - Semantic   │          │
│  │              │  │              │  │   search     │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
│                                                                   │
│  ┌──────────────┐  ┌──────────────┐                             │
│  │ CMS          │  │ Object       │                             │
│  │ (Strapi)     │  │ Storage      │                             │
│  │              │  │ (S3/GCS)     │                             │
│  │ - Content    │  │              │                             │
│  │   management │  │ - Documents  │                             │
│  │              │  │ - Images     │                             │
│  └──────────────┘  └──────────────┘                             │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                   EXTERNAL SERVICES                              │
│                                                                   │
│  - Google Cloud Speech API (STT/TTS)                            │
│  - Anthropic Claude API (NLP)                                   │
│  - Google Maps API (Office locations)                           │
│  - Email Service (SendGrid/SES)                                 │
│  - Analytics (Google Analytics / Plausible)                     │
└─────────────────────────────────────────────────────────────────┘
```

### 1.3 Data Flow - User Journey

**Scenario:** User asks "Mujhe ration card chahiye" (I need a ration card)

```
┌─────────────┐
│ USER        │ Speaks in Hindi via microphone
│             │
└─────┬───────┘
      │
      ↓ (1) Voice recording sent to AI Service
┌─────────────────────────────┐
│ AI SERVICE                  │
│ - Receives audio buffer     │
│ - Calls Google Cloud STT    │
└─────┬───────────────────────┘
      │
      ↓ (2) Transcription: "Mujhe ration card chahiye"
┌─────────────────────────────┐
│ NLP ENGINE (Claude)         │
│ - Extracts intent: "apply"  │
│ - Extracts entity: "ration" │
│ - Language: Hindi           │
└─────┬───────────────────────┘
      │
      ↓ (3) Query eligibility & schemes
┌─────────────────────────────┐
│ ELIGIBILITY MATCHER         │
│ - Semantic search in Vector │
│   DB: "ration card"         │
│ - SQL query in PostgreSQL   │
│   for PDS schemes           │
└─────┬───────────────────────┘
      │
      ↓ (4) Matched schemes returned
┌─────────────────────────────┐
│ RESPONSE GENERATOR (Claude) │
│ - Generate helpful response │
│ - Explain eligibility       │
│ - Provide next steps        │
│ - Format in simple Hindi    │
└─────┬───────────────────────┘
      │
      ↓ (5) Text response
┌─────────────────────────────┐
│ TEXT-TO-SPEECH (Google TTS) │
│ - Convert to Hindi audio    │
│ - Natural female voice      │
└─────┬───────────────────────┘
      │
      ↓ (6) Audio + Text sent to user
┌─────────────┐
│ USER        │ Hears response + sees text
│             │
└─────────────┘
```

---

## 2. User Interface Design

### 2.1 Design Principles

1. **Mobile-First**: Design for small screens first, then scale up
2. **Clarity Over Cleverness**: Simple, obvious UI; no unnecessary animations
3. **Accessibility**: High contrast, large touch targets, screen reader support
4. **Local Language First**: Hindi/local language prominent, English secondary
5. **Offline-Friendly**: Graceful degradation when internet is slow
6. **Low Data Usage**: Minimize images, optimize assets

### 2.2 Visual Design System

#### Color Palette

```
Primary Colors:
- Primary Blue:    #1E40AF (Government trust, professionalism)
- Primary Green:   #059669 (Success, approval)
- Primary Orange:  #EA580C (Call-to-action, urgency)

Neutral Colors:
- Dark Gray:       #1F2937 (Text)
- Medium Gray:     #6B7280 (Secondary text)
- Light Gray:      #F3F4F6 (Background)
- White:           #FFFFFF

Semantic Colors:
- Success:         #10B981
- Warning:         #F59E0B
- Error:           #EF4444
- Info:            #3B82F6
```

#### Typography

```
Primary Font: Noto Sans (supports Hindi, Tamil, Telugu, etc.)
Fallback: system-ui, sans-serif

Heading 1: 32px / 2rem, Bold (Mobile: 24px / 1.5rem)
Heading 2: 24px / 1.5rem, Bold (Mobile: 20px / 1.25rem)
Heading 3: 20px / 1.25rem, Semibold (Mobile: 18px / 1.125rem)
Body Large: 18px / 1.125rem, Regular
Body: 16px / 1rem, Regular
Body Small: 14px / 0.875rem, Regular
Caption: 12px / 0.75rem, Regular

Line Height: 1.6 for body text (better readability)
```

#### Spacing System

```
Base unit: 4px

xs:  4px  (0.25rem)
sm:  8px  (0.5rem)
md:  16px (1rem)
lg:  24px (1.5rem)
xl:  32px (2rem)
2xl: 48px (3rem)
3xl: 64px (4rem)
```

#### Component Sizes

```
Button Height:
- Small: 32px
- Medium: 40px
- Large: 48px (Primary CTA)

Input Height:
- Standard: 48px (easy to tap on mobile)

Touch Target:
- Minimum: 44x44px (iOS guideline)
- Recommended: 48x48px
```

### 2.3 Page Layouts & Wireframes

#### 2.3.1 Homepage

```
┌────────────────────────────────────────────┐
│ [Logo]           [Language: हिन्दी ▼]      │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│     अपनी योजना खोजें                        │
│     Find Your Scheme                        │
│                                             │
│  ┌────────────────────────────────────┐    │
│  │ 🔍 Search schemes...               │    │
│  └────────────────────────────────────┘    │
│                                             │
│  [ 🎤 Voice Search ]                        │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│  Browse by State (राज्य चुनें):            │
│                                             │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐      │
│  │Maharashtra│ │Tamil Nadu│ │Uttar    │     │
│  │         │ │         │ │Pradesh  │     │
│  └─────────┘ └─────────┘ └─────────┘      │
│                                             │
│  [See All States →]                         │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│  National Schemes (राष्ट्रीय योजनाएं):     │
│                                             │
│  ┌──────────────────────────────────┐      │
│  │ 🌾 PM-KISAN                      │      │
│  │ Direct income for farmers        │      │
│  │ [Learn More →]                   │      │
│  └──────────────────────────────────┘      │
│                                             │
│  ┌──────────────────────────────────┐      │
│  │ 🏥 Ayushman Bharat               │      │
│  │ Free health insurance            │      │
│  │ [Learn More →]                   │      │
│  └──────────────────────────────────┘      │
│                                             │
│  [View All National Schemes →]              │
│                                             │
├────────────────────────────────────────────┤
│ Footer: About | Help | Privacy | Contact   │
└────────────────────────────────────────────┘
```

**Design Notes:**
- Hero section with voice search prominently displayed
- Bilingual labels (Hindi first, English below)
- Large, tap-friendly state cards
- Featured national schemes (top 3-5)
- Minimal text, maximum clarity

---

#### 2.3.2 State Page (e.g., Maharashtra)

```
┌────────────────────────────────────────────┐
│ [< Back]    महाराष्ट्र (Maharashtra)       │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│  ┌────────────────────────────────────┐    │
│  │ 🔍 Search schemes in Maharashtra   │    │
│  └────────────────────────────────────┘    │
│                                             │
│  Filter by Category:                        │
│  [ All ] [ Health ] [ Education ]           │
│  [ Employment ] [ Agriculture ] [ More... ] │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│  Active Schemes (120 schemes found)         │
│                                             │
│  ┌──────────────────────────────────┐      │
│  │ 📚 Rajarshi Shahu Scholarship     │      │
│  │ Category: Education               │      │
│  │ For: SC/ST students               │      │
│  │ Benefits: ₹10,000 - ₹60,000      │      │
│  │                                   │      │
│  │ [View Details →]                  │      │
│  └──────────────────────────────────┘      │
│                                             │
│  ┌──────────────────────────────────┐      │
│  │ 🌾 Shetkari Sanman Yojana         │      │
│  │ Category: Agriculture             │      │
│  │ For: Farmers                      │      │
│  │ Benefits: ₹6,000/year             │      │
│  │                                   │      │
│  │ [View Details →]                  │      │
│  └──────────────────────────────────┘      │
│                                             │
│  [Load More]                                │
│                                             │
└────────────────────────────────────────────┘
```

**Design Notes:**
- Breadcrumb navigation (< Back)
- Persistent search bar
- Horizontal scrolling category filters
- Card-based scheme listing
- Key info visible at a glance (category, eligibility, benefits)

---

#### 2.3.3 Scheme Detail Page

```
┌────────────────────────────────────────────┐
│ [< Maharashtra]                             │
│                                             │
│ 📚 Rajarshi Shahu Scholarship              │
│    (राजर्षी शाहू महाराज शिक्षणवृत्ती)      │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ Overview                                    │
│ ─────────────────                           │
│ This scholarship supports SC/ST/OBC        │
│ students pursuing higher education.        │
│ Financial assistance ranges from ₹10,000   │
│ to ₹60,000 based on course level.         │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ Am I Eligible? (क्या मैं पात्र हूं?)        │
│ ─────────────────────────────              │
│ ✓ You belong to SC/ST/OBC category         │
│ ✓ Your family income < ₹8 lakh/year       │
│ ✓ You are studying in college/university   │
│ ✓ You are a resident of Maharashtra        │
│                                             │
│ [Check My Eligibility with AI 🎤]           │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ Required Documents                          │
│ ─────────────────────                       │
│ □ Caste Certificate                         │
│ □ Income Certificate (< ₹8L)               │
│ □ Aadhaar Card                              │
│ □ College ID / Admission Letter            │
│ □ Bank Account Details                      │
│                                             │
│ [Download Checklist PDF]                    │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ How to Apply (कैसे आवेदन करें)              │
│ ─────────────────────────────              │
│                                             │
│ 1️⃣ Collect all required documents          │
│    (Estimated time: 2-3 weeks)             │
│                                             │
│ 2️⃣ Register on Mahadbt portal              │
│    Link: mahadbt.maharashtra.gov.in        │
│                                             │
│ 3️⃣ Fill application form online            │
│    (Takes ~30 minutes)                     │
│                                             │
│ 4️⃣ Upload scanned documents                │
│                                             │
│ 5️⃣ Submit and note application number      │
│                                             │
│ [Get Step-by-Step Voice Guidance 🎤]        │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ Important Details                           │
│ ─────────────────────                       │
│ Application Opens: 1st August              │
│ Deadline: 30th November                    │
│ Processing Time: 2-3 months                │
│                                             │
│ Contact for Help:                          │
│ District Social Welfare Officer            │
│ [Find Nearest Office 📍]                    │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ ┌──────────────────────────────────┐      │
│ │  🎯 Ready to Apply?               │      │
│ │                                   │      │
│ │  [Apply on Official Website →]    │      │
│ │  External link: mahadbt.gov.in    │      │
│ └──────────────────────────────────┘      │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│ Still confused? (अभी भी संशय है?)           │
│ Ask our AI assistant in your language      │
│                                             │
│ [Start Voice Chat 🎤]                       │
│                                             │
└────────────────────────────────────────────┘
```

**Design Notes:**
- Clear, scannable sections
- Eligibility presented as simple checklist
- Visual step-by-step process
- Multiple CTAs for AI assistance
- Official link clearly marked as external

---

#### 2.3.4 AI Voice Assistant Interface

```
┌────────────────────────────────────────────┐
│ [X Close]      AI Assistant                 │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│  🎤 Speak in your language                 │
│     (Hindi, English, or 6 other languages) │
│                                             │
│  ┌────────────────────────────────────┐    │
│  │                                     │    │
│  │         ┌──────────┐               │    │
│  │         │   🎤    │               │    │
│  │         │         │               │    │
│  │         │ Tap to  │               │    │
│  │         │ Speak   │               │    │
│  │         └──────────┘               │    │
│  │                                     │    │
│  │  Or type your question below:      │    │
│  │  ┌──────────────────────────┐      │    │
│  │  │ Type here...             │      │    │
│  │  └──────────────────────────┘      │    │
│  │                                     │    │
│  └────────────────────────────────────┘    │
│                                             │
│  Examples:                                  │
│  • "Mujhe ration card chahiye"             │
│  • "I need scholarship for my daughter"    │
│  • "खेती के लिए कोई योजना है?"              │
│                                             │
├────────────────────────────────────────────┤
│                                             │
│  Conversation:                              │
│                                             │
│  ┌────────────────────────────────────┐    │
│  │ 👤 You (audio playing...)          │    │
│  │ "Mujhe ration card chahiye"        │    │
│  └────────────────────────────────────┘    │
│                                             │
│  ┌────────────────────────────────────┐    │
│  │ 🤖 Assistant                        │    │
│  │                                     │    │
│  │ आप ration card के लिए apply कर    │    │
│  │ सकते हैं। आपको नज़दीकी Panchayat   │    │
│  │ Office जाना होगा।                   │    │
│  │                                     │    │
│  │ ज़रूरी documents:                   │    │
│  │ • Aadhaar Card                      │    │
│  │ • Address Proof                     │    │
│  │ • Income Certificate                │    │
│  │                                     │    │
│  │ [🔊 Play Audio] [📋 Copy]           │    │
│  └────────────────────────────────────┘    │
│                                             │
│  ┌────────────────────────────────────┐    │
│  │ Helpful links:                      │    │
│  │ • PDS Scheme Details                │    │
│  │ • Find Panchayat Office             │    │
│  └────────────────────────────────────┘    │
│                                             │
│  [🎤 Ask Follow-up Question]                │
│                                             │
└────────────────────────────────────────────┘
```

**Design Notes:**
- Large, obvious microphone button
- Voice/text input options
- Conversation bubbles with timestamps
- Audio playback for responses
- Quick action buttons (copy, share)
- Related links embedded in responses

---

### 2.4 Responsive Design Breakpoints

```
Mobile (Portrait):  320px - 767px
Tablet (Portrait):  768px - 1023px
Desktop:            1024px+

Layout Adjustments:

Mobile:
- Single column
- Stacked navigation
- Full-width cards
- Bottom nav bar (if used)

Tablet:
- 2 column grid for scheme cards
- Side drawer navigation
- Larger touch targets

Desktop:
- 3 column grid for scheme cards
- Top navigation bar
- Sidebar for filters
- More content visible
```

### 2.5 Accessibility Features

1. **Keyboard Navigation**
   - All interactive elements accessible via Tab
   - Visible focus indicators (2px blue outline)
   - Skip to main content link

2. **Screen Reader Support**
   - Semantic HTML (header, nav, main, article, footer)
   - ARIA labels for all icons
   - Alt text for all images
   - Live regions for dynamic content

3. **Visual Accessibility**
   - Contrast ratio ≥4.5:1 for text
   - Text resizable up to 200%
   - No color-only indicators (use icons + text)
   - Focus visible at all times

4. **Voice Assistance**
   - Voice input as primary interaction method
   - Audio output for all responses
   - Transcript always visible

---

## 3. Database Design

### 3.1 Entity Relationship Diagram

```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│  schemes    │────────>│ categories  │         │   states    │
│             │ n:1     │             │         │             │
│ • id        │         │ • id        │         │ • code      │
│ • name_*    │         │ • name_*    │         │ • name_*    │
│ • desc_*    │         │ • slug      │         │             │
│ • category  │         └─────────────┘         └─────────────┘
│ • state     │                                         ↑
│ • level     │                                         │ n:1
│ • criteria  │                                         │
│ • docs      │         ┌─────────────┐                │
│ • url       │────────>│  documents  │                │
│ • deadline  │ n:m     │             │                │
│ • benefits  │         │ • id        │                │
└─────────────┘         │ • name_*    │                │
      │                 │ • desc_*    │                │
      │ n:m             │ • obtain    │                │
      │                 └─────────────┘                │
      ↓                                                 │
┌─────────────┐         ┌─────────────┐                │
│scheme_docs  │         │   offices   │────────────────┘
│             │         │             │
│• scheme_id  │         │ • id        │
│• doc_id     │         │ • name      │
└─────────────┘         │ • type      │
      ↑                 │ • state     │
      │ n:m             │ • district  │
      ↓                 │ • address   │
┌─────────────┐         │ • phone     │
│scheme_office│         │ • lat/lng   │
│             │         └─────────────┘
│• scheme_id  │
│• office_id  │
└─────────────┘

┌─────────────────┐     ┌─────────────────┐
│ user_sessions   │     │  analytics      │
│                 │     │                 │
│ • session_id    │     │ • id            │
│ • user_id       │     │ • event_type    │
│ • language      │     │ • scheme_id     │
│ • state         │     │ • user_id       │
│ • conversation  │     │ • timestamp     │
│ • extracted     │     │ • metadata      │
│ • ttl           │     └─────────────────┘
└─────────────────┘
```

### 3.2 Schema Definitions (PostgreSQL)

#### 3.2.1 Core Tables

```sql
-- States table
CREATE TABLE states (
    code VARCHAR(2) PRIMARY KEY,  -- MH, TN, UP, etc.
    name_en VARCHAR(100) NOT NULL,
    name_hi VARCHAR(100),
    name_local VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Categories table
CREATE TABLE categories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    slug VARCHAR(50) UNIQUE NOT NULL,  -- health, education, agriculture
    name_en VARCHAR(100) NOT NULL,
    name_hi VARCHAR(100),
    icon VARCHAR(50),  -- emoji or icon name
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Schemes table (main table)
CREATE TABLE schemes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    
    -- Basic info
    name_en TEXT NOT NULL,
    name_hi TEXT,
    name_local TEXT,
    description_en TEXT NOT NULL,
    description_hi TEXT,
    description_local TEXT,
    
    -- Classification
    category_id UUID REFERENCES categories(id),
    level VARCHAR(20) NOT NULL CHECK (level IN ('state', 'national')),
    state_code VARCHAR(2) REFERENCES states(code),  -- NULL for national
    
    -- Eligibility (JSONB for flexibility)
    eligibility_criteria JSONB NOT NULL,
    /*
    Example structure:
    {
      "age": {"min": 18, "max": 60},
      "income": {"max": 200000, "currency": "INR", "period": "annual"},
      "occupation": ["farmer", "daily wage worker"],
      "residence": ["maharashtra"],  -- or ["all"] for national
      "gender": ["all"],  -- or ["female"], ["male"]
      "caste": ["SC", "ST", "OBC"],  -- or ["all"]
      "special": ["Has disability", "Head of household"]
    }
    */
    
    -- Benefits
    benefits JSONB,
    /*
    {
      "financial": "₹6,000 per year",
      "other": ["Free health insurance", "Skill training"]
    }
    */
    
    -- Application info
    application_url TEXT,
    application_process TEXT,  -- Detailed steps
    deadline DATE,
    
    -- Metadata
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_by UUID,  -- Admin user ID
    
    -- Search optimization
    search_vector tsvector GENERATED ALWAYS AS (
        to_tsvector('english', 
            coalesce(name_en, '') || ' ' || 
            coalesce(description_en, '')
        )
    ) STORED,
    
    -- Indexing
    CONSTRAINT valid_state_or_national CHECK (
        (level = 'state' AND state_code IS NOT NULL) OR
        (level = 'national' AND state_code IS NULL)
    )
);

CREATE INDEX idx_schemes_category ON schemes(category_id);
CREATE INDEX idx_schemes_state ON schemes(state_code);
CREATE INDEX idx_schemes_active ON schemes(is_active);
CREATE INDEX idx_schemes_search ON schemes USING GIN(search_vector);
CREATE INDEX idx_schemes_eligibility ON schemes USING GIN(eligibility_criteria);
```

#### 3.2.2 Supporting Tables

```sql
-- Documents master list
CREATE TABLE documents (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name_en VARCHAR(100) NOT NULL,
    name_hi VARCHAR(100),
    description_en TEXT,
    description_hi TEXT,
    how_to_obtain_en TEXT,
    how_to_obtain_hi TEXT,
    typical_cost VARCHAR(50),  -- "Free" or "₹50"
    processing_time VARCHAR(50),  -- "1-2 weeks"
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Scheme-Document mapping (many-to-many)
CREATE TABLE scheme_documents (
    scheme_id UUID REFERENCES schemes(id) ON DELETE CASCADE,
    document_id UUID REFERENCES documents(id) ON DELETE CASCADE,
    is_mandatory BOOLEAN DEFAULT true,
    notes TEXT,  -- Additional info specific to this scheme
    PRIMARY KEY (scheme_id, document_id)
);

-- Government offices
CREATE TABLE offices (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(200) NOT NULL,
    type VARCHAR(50) NOT NULL,  -- panchayat, municipal, district, specialized
    state_code VARCHAR(2) REFERENCES states(code),
    district VARCHAR(100),
    city VARCHAR(100),
    address TEXT NOT NULL,
    phone VARCHAR(20),
    email VARCHAR(100),
    website VARCHAR(200),
    latitude DECIMAL(10, 8),
    longitude DECIMAL(11, 8),
    working_hours JSONB,
    /*
    {
      "weekdays": "9:00 AM - 5:00 PM",
      "saturday": "9:00 AM - 1:00 PM",
      "sunday": "Closed"
    }
    */
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_offices_state ON offices(state_code);
CREATE INDEX idx_offices_district ON offices(district);
CREATE INDEX idx_offices_location ON offices(latitude, longitude);

-- Scheme-Office mapping (many-to-many)
CREATE TABLE scheme_offices (
    scheme_id UUID REFERENCES schemes(id) ON DELETE CASCADE,
    office_id UUID REFERENCES offices(id) ON DELETE CASCADE,
    PRIMARY KEY (scheme_id, office_id)
);
```

#### 3.2.3 Session & Analytics Tables

```sql
-- User sessions (for AI conversations)
CREATE TABLE user_sessions (
    session_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id VARCHAR(100),  -- Anonymous ID (could be IP hash or device ID)
    language VARCHAR(10) NOT NULL,  -- hi, en, ta, etc.
    state_code VARCHAR(2),
    conversation_history JSONB,
    /*
    [
      {"role": "user", "message": "ration card chahiye", "timestamp": "..."},
      {"role": "assistant", "message": "...", "timestamp": "..."}
    ]
    */
    extracted_profile JSONB,
    /*
    {
      "occupation": "farmer",
      "age": 35,
      "income": "< 2 lakh",
      "has_children": true,
      "documents_available": ["aadhaar"]
    }
    */
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP DEFAULT (CURRENT_TIMESTAMP + INTERVAL '1 hour')
);

CREATE INDEX idx_sessions_expires ON user_sessions(expires_at);

-- Analytics events
CREATE TABLE analytics (
    id BIGSERIAL PRIMARY KEY,
    event_type VARCHAR(50) NOT NULL,  -- page_view, search, scheme_view, ai_query
    scheme_id UUID REFERENCES schemes(id),
    user_id VARCHAR(100),
    session_id UUID,
    metadata JSONB,
    /*
    {
      "search_query": "ration card",
      "results_count": 5,
      "clicked_result": 2,
      "device": "mobile",
      "browser": "Chrome"
    }
    */
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_analytics_event ON analytics(event_type);
CREATE INDEX idx_analytics_scheme ON analytics(scheme_id);
CREATE INDEX idx_analytics_timestamp ON analytics(timestamp);

-- AI feedback
CREATE TABLE ai_feedback (
    id BIGSERIAL PRIMARY KEY,
    session_id UUID REFERENCES user_sessions(session_id),
    message_index INT,  -- Which message in conversation
    rating VARCHAR(10),  -- thumbs_up, thumbs_down
    comment TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 3.2.4 Admin Tables

```sql
-- Admin users
CREATE TABLE admin_users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(100) NOT NULL,
    role VARCHAR(20) NOT NULL CHECK (role IN ('super_admin', 'state_admin', 'editor', 'viewer')),
    state_code VARCHAR(2) REFERENCES states(code),  -- For state_admin role
    is_active BOOLEAN DEFAULT true,
    last_login TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Audit log
CREATE TABLE audit_log (
    id BIGSERIAL PRIMARY KEY,
    admin_id UUID REFERENCES admin_users(id),
    action VARCHAR(50) NOT NULL,  -- create, update, delete
    entity_type VARCHAR(50) NOT NULL,  -- scheme, office, document
    entity_id UUID,
    changes JSONB,  -- Old vs new values
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_audit_admin ON audit_log(admin_id);
CREATE INDEX idx_audit_timestamp ON audit_log(timestamp);
```

### 3.3 Sample Data

```sql
-- Insert sample state
INSERT INTO states (code, name_en, name_hi) VALUES 
('MH', 'Maharashtra', 'महाराष्ट्र'),
('TN', 'Tamil Nadu', 'तमिल नाडु');

-- Insert sample category
INSERT INTO categories (slug, name_en, name_hi, icon) VALUES 
('education', 'Education', 'शिक्षा', '📚'),
('health', 'Health', 'स्वास्थ्य', '🏥'),
('agriculture', 'Agriculture', 'कृषि', '🌾');

-- Insert sample scheme
INSERT INTO schemes (
    name_en, name_hi, 
    description_en, description_hi,
    category_id, level, state_code,
    eligibility_criteria,
    benefits,
    application_url,
    deadline
) VALUES (
    'Rajarshi Shahu Maharaj Scholarship',
    'राजर्षी शाहू महाराज छात्रवृत्ती',
    'Financial assistance for SC/ST/OBC students in higher education',
    'उच्च शिक्षा में SC/ST/OBC छात्रों के लिए वित्तीय सहायता',
    (SELECT id FROM categories WHERE slug = 'education'),
    'state',
    'MH',
    '{
        "age": {"min": 16, "max": 35},
        "income": {"max": 800000, "currency": "INR", "period": "annual"},
        "caste": ["SC", "ST", "OBC"],
        "residence": ["MH"],
        "education": ["college", "university"]
    }'::jsonb,
    '{
        "financial": "₹10,000 - ₹60,000 per year",
        "other": ["Textbook allowance", "Hostel fees"]
    }'::jsonb,
    'https://mahadbt.maharashtra.gov.in',
    '2026-11-30'
);

-- Insert sample document
INSERT INTO documents (name_en, name_hi, description_en, how_to_obtain_en) VALUES
('Aadhaar Card', 'आधार कार्ड', '12-digit unique identity number', 'Visit nearest Aadhaar enrollment center with proof of identity and address'),
('Income Certificate', 'आय प्रमाणपत्र', 'Certificate showing annual family income', 'Apply at Tehsil office with salary slips or affidavit');

-- Link document to scheme
INSERT INTO scheme_documents (scheme_id, document_id, is_mandatory) VALUES
((SELECT id FROM schemes WHERE name_en LIKE 'Rajarshi%'),
 (SELECT id FROM documents WHERE name_en = 'Aadhaar Card'),
 true);
```

### 3.4 Indexes & Performance Optimization

```sql
-- Full-text search index
CREATE INDEX idx_schemes_fulltext ON schemes USING GIN(
    to_tsvector('english', name_en || ' ' || description_en)
);

-- Eligibility search (for common queries)
CREATE INDEX idx_schemes_occupation ON schemes 
    USING GIN((eligibility_criteria->'occupation'));

CREATE INDEX idx_schemes_income ON schemes 
    ((eligibility_criteria->'income'->>'max'));

-- Composite indexes for common queries
CREATE INDEX idx_schemes_state_category ON schemes(state_code, category_id)
    WHERE is_active = true;

-- Partitioning analytics table by month (for large-scale deployment)
CREATE TABLE analytics_2026_02 PARTITION OF analytics
    FOR VALUES FROM ('2026-02-01') TO ('2026-03-01');
```

---

## 4. API Design

### 4.1 REST API Specification

**Base URL:** `https://api.example.com/v1`

**Authentication:**
- Public APIs: No auth required
- Admin APIs: Bearer token (JWT)

**Response Format:**
```json
{
  "success": true,
  "data": { ... },
  "error": null,
  "timestamp": "2026-02-05T10:30:00Z"
}
```

**Error Format:**
```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "SCHEME_NOT_FOUND",
    "message": "Scheme with ID xyz not found",
    "details": {}
  },
  "timestamp": "2026-02-05T10:30:00Z"
}
```

### 4.2 Public API Endpoints

#### 4.2.1 States & Categories

```
GET /states
Description: List all states
Response:
{
  "success": true,
  "data": [
    {
      "code": "MH",
      "name": {
        "en": "Maharashtra",
        "hi": "महाराष्ट्र"
      }
    }
  ]
}

GET /categories
Description: List all scheme categories
Response:
{
  "success": true,
  "data": [
    {
      "id": "uuid",
      "slug": "education",
      "name": {
        "en": "Education",
        "hi": "शिक्षा"
      },
      "icon": "📚"
    }
  ]
}
```

#### 4.2.2 Schemes

```
GET /schemes
Query Parameters:
  - state: State code (MH, TN, etc.)
  - category: Category ID
  - level: state | national
  - active: true | false
  - limit: Number (default: 20, max: 100)
  - offset: Number (for pagination)
  
Response:
{
  "success": true,
  "data": {
    "schemes": [
      {
        "id": "uuid",
        "name": {
          "en": "Rajarshi Shahu Scholarship",
          "hi": "राजर्षी शाहू छात्रवृत्ती"
        },
        "description": {
          "en": "Financial assistance...",
          "hi": "वित्तीय सहायता..."
        },
        "category": {
          "id": "uuid",
          "name": "Education",
          "icon": "📚"
        },
        "level": "state",
        "state": "MH",
        "benefits": {
          "financial": "₹10,000 - ₹60,000"
        },
        "deadline": "2026-11-30",
        "isActive": true
      }
    ],
    "total": 120,
    "limit": 20,
    "offset": 0
  }
}

GET /schemes/:id
Description: Get detailed scheme information
Response:
{
  "success": true,
  "data": {
    "id": "uuid",
    "name": { ... },
    "description": { ... },
    "category": { ... },
    "eligibility": {
      "age": {"min": 16, "max": 35},
      "income": {"max": 800000},
      "caste": ["SC", "ST", "OBC"]
    },
    "documents": [
      {
        "id": "uuid",
        "name": {"en": "Aadhaar Card"},
        "isMandatory": true
      }
    ],
    "offices": [
      {
        "id": "uuid",
        "name": "District Social Welfare Office",
        "address": "...",
        "phone": "..."
      }
    ],
    "applicationUrl": "https://...",
    "applicationProcess": "Step 1...",
    "deadline": "2026-11-30"
  }
}

GET /search
Query Parameters:
  - q: Search query (required)
  - state: Filter by state
  - category: Filter by category
  - lang: Language for results (en, hi)
  
Response:
{
  "success": true,
  "data": {
    "results": [
      {
        "id": "uuid",
        "name": "...",
        "description": "...",
        "relevanceScore": 0.95,
        "highlights": "...ration <mark>card</mark>..."
      }
    ],
    "total": 15,
    "query": "ration card"
  }
}
```

#### 4.2.3 Offices

```
GET /offices
Query Parameters:
  - state: State code
  - district: District name
  - type: Office type
  - lat, lng, radius: Location-based search
  
Response:
{
  "success": true,
  "data": [
    {
      "id": "uuid",
      "name": "Pune Panchayat Office",
      "type": "panchayat",
      "address": "...",
      "phone": "+91-20-12345678",
      "location": {
        "lat": 18.5204,
        "lng": 73.8567
      },
      "workingHours": {
        "weekdays": "9 AM - 5 PM"
      }
    }
  ]
}
```

### 4.3 AI Assistant API Endpoints

```
POST /ai/voice-input
Description: Send voice recording for processing
Request:
  Content-Type: multipart/form-data
  Body:
    - audio: File (wav, mp3)
    - sessionId: UUID (optional)
    - language: String (hi, en)
    
Response:
{
  "success": true,
  "data": {
    "sessionId": "uuid",
    "transcription": "Mujhe ration card chahiye",
    "intent": "apply_for_scheme",
    "entities": {
      "scheme_type": "ration_card",
      "language": "hindi"
    }
  }
}

POST /ai/text-input
Description: Send text query
Request:
{
  "message": "I need a ration card",
  "sessionId": "uuid",
  "language": "en"
}

Response:
{
  "success": true,
  "data": {
    "sessionId": "uuid",
    "response": {
      "text": "To apply for a ration card...",
      "audio": "https://cdn.example.com/audio/response.mp3"
    },
    "suggestedSchemes": [
      {
        "id": "uuid",
        "name": "Public Distribution System",
        "relevance": "high"
      }
    ],
    "nextSteps": [
      "Collect Aadhaar card",
      "Visit nearest Panchayat office"
    ]
  }
}

POST /ai/check-eligibility
Description: Check user eligibility for schemes
Request:
{
  "userProfile": {
    "age": 30,
    "occupation": "farmer",
    "income": 150000,
    "state": "MH",
    "hasChildren": true
  },
  "schemeId": "uuid" // Optional: check specific scheme
}

Response:
{
  "success": true,
  "data": {
    "eligible": true,
    "confidence": "high",
    "matchingCriteria": ["occupation", "income", "residence"],
    "missingInfo": [],
    "explanation": "You are eligible because you are a farmer with income below ₹2 lakh..."
  }
}

GET /ai/session/:sessionId
Description: Get conversation history
Response:
{
  "success": true,
  "data": {
    "sessionId": "uuid",
    "messages": [
      {
        "role": "user",
        "content": "Mujhe scholarship chahiye",
        "timestamp": "2026-02-05T10:00:00Z"
      },
      {
        "role": "assistant",
        "content": "...",
        "timestamp": "2026-02-05T10:00:03Z"
      }
    ],
    "extractedProfile": {
      "needs": ["scholarship"],
      "state": "MH"
    }
  }
}

POST /ai/feedback
Description: Submit feedback on AI response
Request:
{
  "sessionId": "uuid",
  "messageIndex": 2,
  "rating": "thumbs_up",
  "comment": "Very helpful!"
}

Response:
{
  "success": true,
  "data": {
    "message": "Thank you for your feedback"
  }
}
```

### 4.4 Admin API Endpoints

```
POST /admin/login
Description: Admin authentication
Request:
{
  "email": "admin@example.com",
  "password": "secure_password"
}

Response:
{
  "success": true,
  "data": {
    "token": "jwt_token",
    "user": {
      "id": "uuid",
      "email": "admin@example.com",
      "role": "state_admin",
      "state": "MH"
    }
  }
}

POST /admin/schemes
Description: Create new scheme
Headers: Authorization: Bearer <token>
Request:
{
  "name": {
    "en": "New Scheme",
    "hi": "नई योजना"
  },
  "description": { ... },
  "category": "uuid",
  "level": "state",
  "state": "MH",
  "eligibility": { ... },
  "documents": ["uuid1", "uuid2"],
  "applicationUrl": "https://..."
}

Response:
{
  "success": true,
  "data": {
    "id": "uuid",
    "message": "Scheme created successfully"
  }
}

PUT /admin/schemes/:id
Description: Update scheme
(Same structure as POST)

DELETE /admin/schemes/:id
Description: Deactivate scheme
Response:
{
  "success": true,
  "data": {
    "message": "Scheme deactivated"
  }
}

POST /admin/schemes/bulk-import
Description: Import schemes from CSV
Request:
  Content-Type: multipart/form-data
  Body:
    - file: CSV file
    
Response:
{
  "success": true,
  "data": {
    "imported": 50,
    "errors": [
      {
        "row": 12,
        "error": "Missing required field: name_en"
      }
    ]
  }
}

GET /admin/analytics
Query Parameters:
  - start_date: YYYY-MM-DD
  - end_date: YYYY-MM-DD
  - metric: page_views | searches | ai_queries
  
Response:
{
  "success": true,
  "data": {
    "metrics": {
      "totalUsers": 15000,
      "activeSchemes": 120,
      "topSchemes": [
        {"id": "uuid", "name": "...", "views": 5000}
      ],
      "searchQueries": [
        {"query": "ration card", "count": 1200}
      ]
    }
  }
}
```

### 4.5 Rate Limiting

```
Public APIs:
- 100 requests/minute per IP
- 1000 requests/hour per IP

AI APIs:
- 20 requests/minute per session
- 100 requests/hour per user

Admin APIs:
- 300 requests/minute per user
```

### 4.6 Caching Strategy

```
Static Content (CDN):
- Scheme pages: 1 hour cache
- Search results: 15 minutes cache
- State/category lists: 24 hours cache

API Responses (Redis):
- GET /schemes: 5 minutes
- GET /schemes/:id: 1 hour
- Search results: 10 minutes

Invalidation:
- On scheme update/create/delete
- Manual purge via admin panel
```

---

## 5. AI Assistant Design

### 5.1 Conversation Flow

```
User Input
    ↓
┌───────────────────────┐
│ Speech Recognition    │
│ (Google Cloud STT)    │
└───────────────────────┘
    ↓
Transcribed Text
    ↓
┌───────────────────────┐
│ Language Detection    │
│ (Auto-detect)         │
└───────────────────────┘
    ↓
┌───────────────────────┐
│ Intent Classification │
│ (Claude)              │
│                       │
│ Intents:              │
│ - find_scheme         │
│ - check_eligibility   │
│ - get_guidance        │
│ - find_office         │
│ - ask_general         │
└───────────────────────┘
    ↓
┌───────────────────────┐
│ Entity Extraction     │
│ (Claude)              │
│                       │
│ Entities:             │
│ - occupation          │
│ - age, income         │
│ - location            │
│ - documents           │
│ - scheme_name         │
└───────────────────────┘
    ↓
┌───────────────────────┐
│ Context Management    │
│ (Session Store)       │
│                       │
│ - Load history        │
│ - Merge new info      │
│ - Update profile      │
└───────────────────────┘
    ↓
┌───────────────────────┐
│ Query Processing      │
│                       │
│ - Semantic search     │
│   (Vector DB)         │
│ - Exact match (SQL)   │
│ - Rank results        │
└───────────────────────┘
    ↓
┌───────────────────────┐
│ Response Generation   │
│ (Claude)              │
│                       │
│ - Explain schemes     │
│ - Simplify language   │
│ - Add next steps      │
│ - Format for voice    │
└───────────────────────┘
    ↓
┌───────────────────────┐
│ Text-to-Speech        │
│ (Google Cloud TTS)    │
└───────────────────────┘
    ↓
Voice Output to User
```

### 5.2 Prompt Engineering

#### System Prompt for Claude

```
You are a helpful government schemes assistant for India. Your role is to help people discover government schemes, check their eligibility, and guide them through the application process.

COMMUNICATION STYLE:
- Be warm, empathetic, and encouraging
- Use simple, conversational language (avoid bureaucratic jargon)
- Speak in the user's chosen language (Hindi, English, or regional)
- Break complex information into small, digestible pieces
- Always provide actionable next steps

CAPABILITIES:
1. Help users find relevant government schemes
2. Explain eligibility criteria in simple terms
3. Provide step-by-step application guidance
4. Answer questions about required documents
5. Find nearby government offices

LIMITATIONS:
- You cannot guarantee eligibility (only provide information)
- You cannot submit applications on behalf of users
- You cannot provide legal advice
- Always direct users to official sources for final verification

RESPONSE FORMAT:
- Keep responses under 150 words for voice output
- Use numbered lists for steps
- Include specific examples when helpful
- End with a clear next action

CURRENT CONTEXT:
{context_from_session}

USER PROFILE:
{extracted_user_info}

AVAILABLE SCHEMES:
{relevant_schemes_from_db}
```

#### Example Interaction

```
User (Hindi): "Main daily wage worker hoon, mujhe koi help chahiye"

Assistant Processing:
1. Intent: find_scheme
2. Entities: {occupation: "daily wage worker"}
3. Context: First message, no prior info
4. Query: Search schemes for "daily wage worker"
5. Results: 5 relevant schemes found

Assistant Response (Hindi):
"Aapके लिए कई योजनाएं हैं! सबसे मददगार तीन:

1. PM-Kisan: ₹6,000/साल किसानों के लिए
2. MGNREGA: 100 दिन का रोज़गार गारंटी
3. Ayushman Bharat: Free स्वास्थ्य बीमा

आप किस बारे में ज़्यादा जानना चाहेंगे?"

[Voice + Text displayed to user]
```

### 5.3 Eligibility Matching Algorithm

```python
def calculate_eligibility(user_profile, scheme):
    """
    Calculate eligibility score and explanation
    """
    score = 0
    max_score = 0
    matching_criteria = []
    missing_criteria = []
    
    criteria = scheme['eligibility_criteria']
    
    # Check age
    if 'age' in criteria:
        max_score += 10
        user_age = user_profile.get('age')
        if user_age:
            if criteria['age']['min'] <= user_age <= criteria['age']['max']:
                score += 10
                matching_criteria.append('age')
            else:
                missing_criteria.append('age')
    
    # Check income
    if 'income' in criteria:
        max_score += 15
        user_income = user_profile.get('income')
        if user_income:
            if user_income <= criteria['income']['max']:
                score += 15
                matching_criteria.append('income')
            else:
                missing_criteria.append('income')
    
    # Check occupation
    if 'occupation' in criteria:
        max_score += 15
        user_occupation = user_profile.get('occupation')
        if user_occupation:
            if user_occupation in criteria['occupation'] or 'all' in criteria['occupation']:
                score += 15
                matching_criteria.append('occupation')
            else:
                missing_criteria.append('occupation')
    
    # Check residence
    if 'residence' in criteria:
        max_score += 10
        user_state = user_profile.get('state')
        if user_state:
            if user_state in criteria['residence'] or 'all' in criteria['residence']:
                score += 10
                matching_criteria.append('residence')
            else:
                missing_criteria.append('residence')
    
    # Calculate final score
    if max_score > 0:
        percentage = (score / max_score) * 100
    else:
        percentage = 0
    
    # Determine confidence level
    if percentage >= 80:
        confidence = "high"
        eligible = True
    elif percentage >= 50:
        confidence = "medium"
        eligible = True
    else:
        confidence = "low"
        eligible = False
    
    return {
        "eligible": eligible,
        "confidence": confidence,
        "score": percentage,
        "matching_criteria": matching_criteria,
        "missing_criteria": missing_criteria
    }
```

### 5.4 Multilingual Support

```python
# Language configuration
SUPPORTED_LANGUAGES = {
    'en': {
        'name': 'English',
        'voice': 'en-IN-Wavenet-D',
        'model': 'claude-3-sonnet'
    },
    'hi': {
        'name': 'हिन्दी',
        'voice': 'hi-IN-Wavenet-D',
        'model': 'claude-3-sonnet'
    },
    'ta': {
        'name': 'தமிழ்',
        'voice': 'ta-IN-Wavenet-A',
        'model': 'claude-3-sonnet'
    },
    # ... more languages
}

# Language detection
async def detect_language(text):
    """
    Detect language from user input
    """
    # Use Claude to detect language
    response = await claude.complete(
        prompt=f"What language is this text in? Just respond with language code (en, hi, ta, etc.): {text}"
    )
    return response.strip()

# Translation (if needed)
async def translate_response(text, target_lang):
    """
    Translate response to target language
    """
    if target_lang == 'en':
        return text
    
    response = await claude.complete(
        prompt=f"Translate this to {target_lang}, keeping it simple and conversational: {text}"
    )
    return response
```

---

## 6. Security Design

### 6.1 Authentication & Authorization

```
Public Website:
- No authentication required for browsing
- Optional user accounts (future feature)

AI Assistant:
- Session-based (anonymous)
- Rate limited per IP
- No PII collected

Admin Panel:
- JWT-based authentication
- Role-based access control (RBAC)
- Session timeout: 30 minutes

Roles & Permissions:
┌──────────────┬─────────┬─────────┬─────────┬──────────┐
│ Action       │ Super   │ State   │ Editor  │ Viewer   │
│              │ Admin   │ Admin   │         │          │
├──────────────┼─────────┼─────────┼─────────┼──────────┤
│ View schemes │ ✓       │ ✓       │ ✓       │ ✓        │
│ Create scheme│ ✓       │ ✓(own)  │ ✓(draft)│ ✗        │
│ Edit scheme  │ ✓       │ ✓(own)  │ ✓(own)  │ ✗        │
│ Delete scheme│ ✓       │ ✓(own)  │ ✗       │ ✗        │
│ Publish      │ ✓       │ ✓(own)  │ ✗       │ ✗        │
│ Manage users │ ✓       │ ✗       │ ✗       │ ✗        │
│ View analytics│ ✓      │ ✓(own)  │ ✓(own)  │ ✓(own)   │
└──────────────┴─────────┴─────────┴─────────┴──────────┘
```

### 6.2 Data Protection

```
Encryption:
- TLS 1.3 for all traffic
- Database encryption at rest (AES-256)
- API keys encrypted in environment variables
- Password hashing: Argon2 (or bcrypt with cost factor 12)

PII Handling:
- No user voice recordings stored permanently
- Conversation logs anonymized after 90 days
- IP addresses hashed for rate limiting
- No email/phone collection without consent

Compliance:
- IT Act 2000 compliance
- GDPR-like principles
- Regular security audits
- Vulnerability scanning
```

### 6.3 Input Validation & Sanitization

```typescript
// Example: API input validation
import { z } from 'zod';

const CreateSchemeSchema = z.object({
  name: z.object({
    en: z.string().min(5).max(200),
    hi: z.string().optional()
  }),
  description: z.object({
    en: z.string().min(20).max(5000),
    hi: z.string().optional()
  }),
  category: z.string().uuid(),
  level: z.enum(['state', 'national']),
  state: z.string().length(2).optional(),
  eligibility: z.object({
    age: z.object({
      min: z.number().min(0).max(100),
      max: z.number().min(0).max(100)
    }).optional(),
    income: z.object({
      max: z.number().positive()
    }).optional()
  }),
  applicationUrl: z.string().url()
});

// Usage
app.post('/admin/schemes', async (req, res) => {
  try {
    const validated = CreateSchemeSchema.parse(req.body);
    // Process validated data
  } catch (error) {
    res.status(400).json({ error: 'Invalid input' });
  }
});
```

---

## 7. Deployment Design

### 7.1 Infrastructure Diagram (AWS)

```
┌─────────────────────────────────────────────────────────┐
│                    ROUTE 53 (DNS)                        │
│                  example.com → CloudFront                │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│                 CLOUDFRONT (CDN)                         │
│  - Static assets (images, CSS, JS)                      │
│  - Edge caching                                          │
│  - SSL/TLS termination                                   │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│         APPLICATION LOAD BALANCER (ALB)                  │
│  - Health checks                                         │
│  - Auto-scaling triggers                                 │
│  - SSL termination (backup)                              │
└─────────────────────────────────────────────────────────┘
                          ↓
        ┌─────────────────┴─────────────────┐
        ↓                                    ↓
┌──────────────────┐              ┌──────────────────┐
│   ECS CLUSTER    │              │  LAMBDA          │
│   (Web App)      │              │  (AI Service)    │
│                  │              │                  │
│  Task Definition:│              │  Runtime: Python │
│  - Next.js app   │              │  Memory: 3GB     │
│  - 2 vCPU        │              │  Timeout: 60s    │
│  - 4GB RAM       │              │                  │
│  - Auto-scale:   │              │  Triggers:       │
│    2-10 tasks    │              │  - API Gateway   │
└──────────────────┘              └──────────────────┘
        ↓                                    ↓
┌─────────────────────────────────────────────────────────┐
│                      DATA LAYER                          │
│                                                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │ RDS         │  │ ElastiCache │  │ S3          │     │
│  │ PostgreSQL  │  │ Redis       │  │             │     │
│  │             │  │             │  │ - Documents │     │
│  │ Multi-AZ    │  │ - Sessions  │  │ - Images    │     │
│  │ Read replica│  │ - Cache     │  │ - Backups   │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
```

### 7.2 CI/CD Pipeline

```
Developer pushes code to GitHub
         ↓
GitHub Actions triggered
         ↓
┌────────────────────────┐
│  BUILD STAGE           │
│  - Run linting         │
│  - Run tests           │
│  - Build Docker image  │
│  - Security scan       │
└────────────────────────┘
         ↓
┌────────────────────────┐
│  STAGING DEPLOYMENT    │
│  - Deploy to staging   │
│  - Run E2E tests       │
│  - Performance tests   │
└────────────────────────┘
         ↓
  Manual approval
         ↓
┌────────────────────────┐
│  PRODUCTION DEPLOYMENT │
│  - Blue-green deploy   │
│  - Health checks       │
│  - Rollback on fail    │
└────────────────────────┘
```

### 7.3 Monitoring & Alerting

```
Metrics to Monitor:
- Application uptime
- API response times (p50, p95, p99)
- Error rates
- Database connections
- Cache hit ratio
- AI API costs
- Voice recognition accuracy

Alerts:
- Uptime < 99.5% → PagerDuty
- Error rate > 1% → Slack
- Response time > 3s → Email
- Database CPU > 80% → Slack
- AI costs > $2000/day → Email

Tools:
- CloudWatch (AWS metrics)
- Datadog (Application monitoring)
- Sentry (Error tracking)
- Grafana (Dashboards)
```

---

**END OF DESIGN DOCUMENT**
