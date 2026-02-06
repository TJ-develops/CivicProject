# Design Document
## Public Information Portal with Voice-First AI Assistant

**Project Name:** Civic Information Portal (Working Title)  
**Submission Date:** February 2026  
**Document Purpose:** Visual design, user experience, and system overview for idea submission

---

## 1. Vision Statement

**We envision a future where every Indian citizen can easily discover and access government schemes they qualify for—regardless of their language, literacy level, or technical skills.**

Our platform makes this vision real by combining:
- **Simple, organized information** (no bureaucratic jargon)
- **Voice-first AI** (speak in your own language)
- **Actionable guidance** (not just information, but clear next steps)

---

## 2. Design Philosophy

### 2.1 Core Principles

**1. Mobile-First, Voice-First**
- Most users will access via smartphones
- Voice should be the primary interaction method (not typing)
- Large, tap-friendly buttons
- Minimal text input required

**2. Accessibility for All**
- Works on basic smartphones (₹5,000 Android phones)
- Works on slow internet (2G/3G)
- Works for users with limited literacy
- Works for users with disabilities (screen readers, high contrast)

**3. Local Language, Local Context**
- Hindi and English from day one
- Regional languages (Tamil, Telugu, Marathi, etc.) added progressively
- All content available in user's preferred language
- Cultural sensitivity in design and messaging

**4. Trust and Transparency**
- Clear sourcing ("According to official Maharashtra government website...")
- Disclaimers visible ("Please verify with official sources")
- No hidden fees, no ads, no commercial motives
- Government partnership logos displayed

**5. Progressive Enhancement**
- Website works perfectly without AI (basic information access)
- AI enhances the experience but isn't required
- Graceful degradation when internet is slow

---

## 3. User Experience Design

### 3.1 User Personas

**Persona 1: Ramesh - The Rural Farmer**
- Age: 45, Village in Maharashtra
- Device: Basic Android smartphone (borrowed from son)
- Language: Marathi (limited English)
- Goal: Find schemes for farmers, crop insurance
- Pain point: Doesn't know what schemes exist

**Persona 2: Lakshmi - The Urban Domestic Worker**
- Age: 38, Chennai
- Language: Tamil (no English)
- Goal: Find scholarship for daughter's college
- Pain point: Confused by eligibility criteria

**Persona 3: Arjun - The Student**
- Age: 20, Semi-urban town in UP
- Language: Hindi, some English
- Goal: Find employment schemes, skill training
- Pain point: Too many schemes, doesn't know which apply

---

## 4. Visual Design

### 4.1 Color Palette

**Primary Colors:**
- 🔵 **Trust Blue** (#1E40AF) - Navigation, government badge
- 🟢 **Success Green** (#059669) - Eligible indicators, active schemes
- 🟠 **Action Orange** (#EA580C) - "Apply Now" buttons, voice button

**Why These Colors:**
- High contrast (readable in bright sunlight)
- Culturally appropriate
- Accessible (WCAG AAA compliant)

### 4.2 Typography

- **Font:** Noto Sans (supports all Indian languages)
- **Sizes:** Large headings (24px mobile), readable body (16px)
- **Bilingual:** Primary language large, secondary smaller

---

## 5. Page Layouts

### 5.1 Homepage (Mobile)

```
┌─────────────────────────────────┐
│  🏛️ Portal        [हिन्दी ▼]   │
├─────────────────────────────────┤
│      अपनी योजना खोजें           │
│      Find Your Scheme           │
│                                 │
│  ┌─────────────────────────┐   │
│  │ 🔍 Search schemes...    │   │
│  └─────────────────────────┘   │
│                                 │
│  ┌─────────────────────────┐   │
│  │   🎤  Speak Your        │   │
│  │      Question           │   │
│  └─────────────────────────┘   │
│                                 │
│  Choose Your State:             │
│  ┌──────┐ ┌──────┐ ┌──────┐   │
│  │  MH  │ │  TN  │ │  UP  │   │
│  └──────┘ └──────┘ └──────┘   │
│                                 │
│  Popular Schemes:               │
│  📄 PM-KISAN → ₹6,000/year      │
│  📄 Ayushman Bharat → Health    │
└─────────────────────────────────┘
```

**Design Choices:**
- Bilingual labels
- Big voice button (most important feature)
- Visual icons for schemes
- Minimal text

### 5.2 Scheme Detail Page

```
┌─────────────────────────────────┐
│  [← Back] Scholarship           │
├─────────────────────────────────┤
│  📚 Rajarshi Shahu Scholarship  │
│     (राजर्षी शाहू छात्रवृत्ती)  │
│                                 │
│  📝 Overview                     │
│  Financial help for SC/ST/OBC   │
│  students. ₹10,000-₹60,000/year │
│                                 │
│  ✅ Am I Eligible?               │
│  ☑ SC/ST/OBC category           │
│  ☑ Family income < ₹8 lakh      │
│  ☑ Studying in college          │
│                                 │
│  📄 Required Documents           │
│  □ Caste Certificate            │
│  □ Income Certificate           │
│  □ Aadhaar Card                 │
│                                 │
│  🗺️ How to Apply                 │
│  1️⃣ Collect documents (2 weeks) │
│  2️⃣ Register on mahadbt.gov.in  │
│  3️⃣ Fill form (30 min)          │
│  4️⃣ Upload documents            │
│                                 │
│  [🎤 Get Voice Guidance]        │
│  [🌐 Apply on Official Site →] │
└─────────────────────────────────┘
```

**Design Choices:**
- Scannable sections
- Emoji icons (universal)
- Numbered steps
- Multiple CTAs

### 5.3 AI Voice Interface

```
┌─────────────────────────────────┐
│  [✕]   AI Assistant             │
├─────────────────────────────────┤
│  🎤 अपनी भाषा में बोलें         │
│     Speak in Your Language      │
│                                 │
│     ┌──────────────────┐        │
│     │      🎤          │        │
│     │   Tap to Speak   │        │
│     └──────────────────┘        │
│                                 │
│  Examples:                      │
│  • "Mujhe ration card chahiye"  │
│  • "खेती के लिए योजना?"         │
│                                 │
├─────────────────────────────────┤
│  Conversation:                  │
│                                 │
│  👤 YOU: "Mujhe ration card     │
│          chahiye"               │
│                                 │
│  🤖 ASSISTANT:                  │
│  "आप ration card के लिए        │
│   apply कर सकते हैं।            │
│                                 │
│   Documents needed:             │
│   • Aadhaar Card                │
│   • Address Proof               │
│                                 │
│   [PDS Scheme →]                │
│   [Find Office →]"              │
│                                 │
│  [🎤 Ask Follow-Up]             │
│  [👍 Helpful] [👎 Not Helpful]  │
└─────────────────────────────────┘
```

---

## 6. System Overview

### 6.1 How It Works (Simple Diagram)

```
CONTENT TEAM
Add schemes in database
        ↓
WEBSITE DATABASE
3,000+ schemes stored
        ↓
USER INTERFACE
Browse by state/search
        ↓
USER ACCESS
Mobile browser/app

VOICE AI FLOW:
User speaks → Speech-to-Text → AI Understanding
→ Search database → Generate response → Text-to-Speech
→ User hears answer
```

### 6.2 Example Data Flow

**Scenario: Finding scholarship**

1. Content team uploads "Rajarshi Scholarship" with details
2. Student visits website → Maharashtra → Education
3. Finds scholarship, checks eligibility
4. OR uses voice: "Mala scholarship pahije" (Marathi)
5. AI searches database, finds relevant schemes
6. AI responds in Marathi with options
7. Student clicks "Apply" → goes to official portal

---

## 7. Content Strategy

### 7.1 Writing Guidelines

**Good Example:**
> "You can get ₹6,000/year if you are a farmer with <2 hectares land. Visit Panchayat office with Aadhaar."

**Bad Example:**
> "Direct income support subject to fulfillment of eligibility criteria as per operational guidelines..."

**Principles:**
- Use "you" (not "beneficiary")
- Use common words (not jargon)
- Use active voice
- Use examples
- Maximum 3 sentences per section

### 7.2 Languages (Priority)

1. Hindi - 40% users
2. English - 30% users  
3. Tamil, Telugu, Marathi, Bengali, Gujarati, Kannada

**Translation Process:**
- Professional translation (not Google Translate)
- Cultural adaptation
- Native speaker review

---

## 8. Accessibility Features

**For Low Vision:**
- High contrast
- Large text (16px minimum)
- Screen reader support

**For Low Literacy:**
- Icons for categories
- Visual progress bars
- Voice-first design
- Maximum 3 sentences per section

**For Low Connectivity:**
- Minimal images
- Compressed files
- Offline mode
- Show cached data if network fails

---

## 9. Trust & Safety

### 9.1 Building Trust

**Source Attribution:**
```
ℹ️ Source: Maharashtra Govt Portal
   Last verified: Feb 1, 2026
   🔗 mahadbt.maharashtra.gov.in
```

**Disclaimers:**
```
⚠️ This info is for guidance only.
   Verify with official sources.
```

**Partnership Logos:**
```
Supported by:
[Digital India] [State Govt] [NGO Partners]
```

### 9.2 Privacy Protection

**What we collect:**
- Which schemes you view
- Your state
- Language preference

**What we DON'T collect:**
- Personal information
- Voice recordings (deleted after use)
- Location beyond state

---

## 10. Success Metrics

### 10.1 Dashboard (for Admins)

```
📊 PLATFORM OVERVIEW (Last 30 Days)

👥 Total Users: 150,000 (↑15%)
🔍 Searches: 45,000
🎤 AI Chats: 12,000 (4.2/5 ⭐)

🌐 Languages:
   Hindi: 45% | English: 30% | Tamil: 15%

🏆 TOP SCHEMES:
1. PM-Kisan - 12,000 views
2. Ayushman Bharat - 9,500 views
3. Ration Card - 8,200 views
```

### 10.2 Impact Tracking

```
100,000 visitors
    ↓
60,000 found scheme (60%)
    ↓
30,000 checked eligibility (50%)
    ↓
15,000 clicked "Apply" (50%)
```

---

## 11. Roadmap

**Year 1:** 2 states, Hindi/English, AI assistant  
**Year 2:** 10 states, 6 languages, mobile app, WhatsApp  
**Year 3:** All states, 10+ languages, IVR system

**Long-term:**
- DigiLocker integration
- AI fills forms
- SMS alerts
- Offline app
- Video tutorials

---

## Conclusion

This design creates a **simple, accessible, trustworthy platform** that bridges the gap between government schemes and people who need them.

**Key Principles:**
✅ Mobile-first, voice-first  
✅ Local language support  
✅ Simple, not simplistic  
✅ Works without AI (better with AI)  
✅ Trust-focused

**Expected Impact:**
- "Much easier than government websites!"
- "I understood everything in my language"
- "AI explained like a helpful friend"
- "Found schemes I didn't know existed"
- "Actually completed my application!"

This can **change millions of lives** by making government benefits truly accessible.

---

**Document Version:** 1.0  
**For:** Idea Submission & Stakeholder Review
