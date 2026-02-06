# Project Requirements Document
## Public Information Portal with Voice-First AI Assistant

NOTE: This document represents a preliminary version of the project specifications.
The requirements and design are subject to change as the idea is further refined, validated, and developed.

**Project Name:** Civic Information Portal (Working Title)  
**Submission Date:** February 2026  

---

## Executive Summary

We propose to build a **state-wise and national public information portal** combined with a **voice-first AI assistant** that helps Indian citizens—especially those in rural, semi-urban, and low-income communities—discover government schemes, understand their eligibility, and get step-by-step guidance to actually access these benefits.

**The Core Problem:** Government schemes exist, but people don't know about them, can't understand the eligibility criteria, and struggle to complete the application process.

**Our Solution:** A simple, accessible platform that organizes all scheme information in one place and adds an AI assistant that speaks the user's language—literally and figuratively.

---

## 1. Problem Statement


### 1.1 The Three-Part Problem

**Problem A: Information is Scattered Everywhere**
- Government schemes are spread across dozens of different websites
- Information is written in bureaucratic English that most people can't understand
- No single place to find what's available in your state
- Rural citizens don't know what exists for them

**Problem B: Eligibility is Confusing**
Even when people find a scheme, they face questions like:
- "Am I actually eligible for this?"
- "Does this apply in my state?"
- "What documents do I need?"
- "Where do I apply?"

**Problem C: Knowing ≠ Doing**
Even eligible people struggle to complete applications because:
- They don't know which office to visit
- They don't know what to say or which papers to bring
- They make avoidable mistakes that delay or reject applications
- No one guides them through the actual process

### 1.2 Who is Affected?

**Primary Users (Target Audience):**
- **Rural citizens** with limited internet access and basic smartphones
- **Daily wage workers, farmers, small vendors** who qualify for many schemes but don't know about them
- **Low-income families** who need government support but can't navigate bureaucracy
- **Semi-literate individuals** who struggle with English and complex forms
- **Regional language speakers** who prefer Hindi, Tamil, Telugu, Marathi, etc.

**Estimated Impact:** 400+ million Indians who qualify for government schemes but don't access them due to information barriers.

---

## 2. Our Solution

### 2.1 Two-Part System

**Part 1: Public Information Website (The Foundation)**
A clean, simple website that works WITHOUT AI. This ensures basic access for everyone.

**What it contains:**
- Every state's active government schemes (Maharashtra, Tamil Nadu, UP, etc.)
- National schemes (PM-Kisan, Ayushman Bharat, Ration Card, etc.)
- Simple language explanations (not bureaucratic jargon)
- Clear eligibility criteria
- Required documents listed
- Official application links
- Nearest government offices with maps
- Available in Hindi, English, and 6+ regional languages

**Part 2: AI Assistant (The Intelligence Layer)**
Voice-first AI that sits on top of the website to make it truly accessible.

**What it does:**
- **Understands natural language:** User can speak in Hindi, Tamil, Telugu, or any supported language
- **Extracts key information:** From "Main daily wage worker hoon, mera ration card nahi bana" the AI understands: occupation = daily wage worker, need = ration card
- **Matches to schemes:** AI searches the database and finds relevant schemes
- **Checks eligibility:** AI compares user's situation against eligibility criteria
- **Provides guidance:** AI gives step-by-step instructions in simple language
- **Answers follow-up questions:** Users can ask "What documents do I need?" or "Where is the nearest office?"

### 2.2 Key Features

#### For General Public:

**Browse by State:**
- Click on your state → See all schemes available in your state
- Filter by category: Health, Education, Employment, Agriculture, Housing, etc.
- Search by keywords: "ration card", "scholarship", "farmer loan"

**Detailed Scheme Pages:**
- Scheme name in local language + English
- Simple description (100-200 words, no jargon)
- "Am I Eligible?" section with checkboxes
- Required documents with explanations
- Step-by-step application process
- Official government link to apply
- Deadline (if applicable)
- Nearest office to visit

**Office Locator:**
- Find Panchayat offices, Municipal offices, District offices
- Shows address, phone number, working hours
- Google Maps integration for directions

**Voice Assistant (AI):**
- Click microphone → Speak your question
- AI responds in your language (voice + text)
- Conversational interface (like talking to a helpful person)
- Remembers context within conversation
- Suggests next steps

---

## 3. Success Metrics & Goals

### 3.1 Phase 1 Goals 

**Scope:**
- Launch in 2 pilot states 
- 100+ schemes per state populated
- AI assistant in Hindi + English only
- Basic website with search functionality


### 3.2 Phase 2 Goals 

**Scope:**
- Expand to multiple states
- Add regional languages 
- Enhanced AI features (better eligibility matching)
- Mobile app for Android


### 3.3 Phase 3 Goals 

**Scope:**
- All 28 states 8 Union Territories
- All major Indian languages 
- WhatsApp integration (reach users where they are)
- IVR system (phone-based voice interface for those without internet)
- Application status tracking


---

## 4. What Makes This Different?

### 4.1 Compared to Existing Government Portals

**Government Portals Today:**
- Complex navigation, technical language
- Separate portal for each state/scheme
- English-only or poor translations
- No assistance in understanding eligibility
- No guidance on actually applying

**Our Platform:**
- Simple, unified interface
- All schemes in one place
- True multilingual support
- AI assistant explains everything in your language
- Step-by-step guidance from discovery to application

### 4.2 Compared to Other Civic Tech Solutions

**Most Civic Tech Tools:**
- Focus on making information "available" (just PDFs online)
- Built for urban, educated users
- No voice interface
- No personalized guidance

**Our Platform:**
- Focus on making information **accessible and actionable**
- Built for rural, low-literacy users
- Voice-first design
- Personalized eligibility matching and guidance
- Progressive enhancement (works without AI, better with AI)

---

## 5. User Journey Examples

### Example 1: Rural Farmer Discovers Crop Insurance

**Ramu is a 45-year-old farmer in Maharashtra with a basic smartphone.**

**Without our platform:**
1. Doesn't know crop insurance schemes exist
2. Never applies, loses crops to unexpected weather
3. Falls into debt

**With our platform:**
1. Village helper tells Ramu about the platform
2. Ramu calls friend who has internet
3. Friend opens website → Clicks Maharashtra → Agriculture
4. Finds "Pradhan Mantri Fasal Bima Yojana" (Crop Insurance)
5. Sees he's eligible (has farmland, has Kisan Credit Card)
6. Reads simple instructions in Marathi
7. Goes to nearest agriculture office with required documents
8. Successfully enrolls in insurance

**OR (with voice AI):**
1. Ramu uses voice assistant on friend's phone
2. Says in Marathi: "Mala pikasathi vimacha pahije" (I need insurance for crops)
3. AI explains crop insurance scheme in Marathi
4. AI tells him exactly what documents to bring and where to go
5. Ramu successfully enrolls

### Example 2: Single Mother Finds Scholarship for Daughter

**Lakshmi is a domestic worker in Chennai, her daughter just completed 12th grade.**

**Without our platform:**
1. Doesn't know scholarships exist for her daughter
2. Daughter can't afford college, dreams deferred

**With our platform:**
1. NGO worker shows Lakshmi the platform
2. Lakshmi clicks Tamil Nadu → Education → Scholarships
3. Finds "Post-Matric Scholarship for SC/ST Students"
4. Sees daughter is eligible (SC category, family income <₹2.5L, 75% marks)
5. Platform lists required documents (caste certificate, income proof, marksheet)
6. Shows step-by-step: "Register on Tamil Nadu scholarship portal → Fill form → Upload documents"
7. Lakshmi helps daughter complete application
8. Daughter gets scholarship, goes to college

---

## 6. Technical Requirements (High-Level)

### 6.1 Website Requirements

**Must Work On:**
- Low-end Android smartphones (2GB RAM)
- 2G/3G networks (not just 4G/5G)
- Screen sizes from 320px to desktop
- All major browsers (Chrome, Firefox, Safari)

**Must Support:**
- Multiple languages (starting with Hindi/English, expanding to 10+ languages)
- Voice input and voice output
- Text search and filters
- Offline capability (future feature)
- Screen readers for visually impaired users

**Performance Requirements:**
- Page load time: <3 seconds on 3G
- Search results: <2 seconds
- Voice transcription: <3 seconds
- AI response: <2 seconds (start streaming)
- Uptime: 99.5% (Phase 1), 99.9% (Phase 3)

### 6.2 AI Assistant Requirements

**Voice Capabilities:**
- Speech-to-text in 10+ Indian languages
- Natural-sounding text-to-speech output
- Background noise tolerance
- Low bandwidth audio (works on 2G/3G)

**Intelligence Capabilities:**
- Understand conversational queries (not just keywords)
- Extract user details (occupation, age, income, location, etc.)
- Match users to relevant schemes (semantic search + exact matching)
- Calculate eligibility with confidence levels
- Generate clear, simple explanations
- Maintain conversation context (remember what user said earlier)
- Handle follow-up questions

**Accuracy Requirements:**
- Voice recognition: ≥85% accurate
- Intent recognition: ≥85% accurate
- Eligibility matching: 90% of top 3 results are relevant
- No false positives (don't tell ineligible users they qualify)

### 6.3 Content Management Requirements

**For Non-Technical Government Staff:**
- Simple web form to add/edit schemes
- No coding knowledge required
- Multi-language editing (side-by-side)
- Bulk upload via CSV/Excel
- Preview before publishing
- Version control (track changes)

**Data Quality:**
- All scheme information verified against official government sources
- Regular updates (at least monthly)
- Outdated schemes marked as inactive within 7 days
- Clear disclaimer: "Verify with official sources before applying"

### 6.4 Privacy & Security Requirements

**Privacy:**
- No voice recordings stored permanently
- No personally identifiable information collected without consent
- Anonymous usage analytics only
- Conversations auto-deleted after 90 days

**Security:**
- Encrypted connections (HTTPS)
- Secure admin panel (password protected)
- Rate limiting (prevent abuse)
- Regular security audits
- Compliance with IT Act 2000

---

## 7. Implementation Approach

### 7.1 Three-Phase Rollout

**Phase 1: Pilot (Months 1-3)**
- **What:** Basic website + AI assistant in 2 states
- **Languages:** Hindi, English
- **Schemes:** 100+ schemes per state
- **Users:** Target 100,000 users
- **Budget:** ~$8,000/month (infrastructure + AI costs)

**Phase 2: Regional Expansion (Months 4-9)**
- **What:** Expand to 8-10 states, add mobile app
- **Languages:** Add Tamil, Telugu, Marathi, Bengali, Gujarati, Kannada
- **Schemes:** 1,000+ total schemes
- **Users:** Target 500,000 users
- **Budget:** ~$15,000/month

**Phase 3: National Scale (Months 10-24)**
- **What:** All states, WhatsApp integration, IVR system
- **Languages:** 10+ Indian languages
- **Schemes:** 3,000+ schemes
- **Users:** Target 5 million users
- **Budget:** ~$30,000/month (potentially offset by government/CSR funding)

### 7.2 Content Sourcing Strategy

**How we'll get scheme data:**
1. **Web scraping:** Automated collection from official government websites
2. **Partnership with state governments:** Request official scheme databases
3. **Manual entry:** Research team populates database from official sources
4. **Crowdsourcing:** NGOs and field workers contribute local scheme knowledge
5. **Regular updates:** Dedicated team monitors changes monthly

**Quality assurance:**
- Every scheme verified against official government portal
- Two-person verification for critical information
- User feedback mechanism to report errors
- Monthly audits of popular schemes

### 7.3 Technology Approach

**Core Technologies:**
- Modern web framework for fast, responsive website
- Cloud infrastructure for reliability and scaling
- AI/ML services for voice and natural language processing
- Database for storing scheme information
- Content management system for easy updates

**Key Vendors/Services:**
- **Cloud hosting:** AWS or Google Cloud
- **Voice AI:** Google Cloud Speech (or equivalent)
- **Language AI:** Claude by Anthropic or GPT-4 by OpenAI
- **Maps:** Google Maps for office locations
- **Analytics:** Standard web analytics tools

**Why these choices:**
- Proven reliability and scale
- Support for Indian languages
- Cost-effective for our budget
- Can handle millions of users

---

## 9. Risks & Mitigation

### 9.1 Key Risks

**Risk 1: Government data is outdated or unavailable**
- **Mitigation:** Start with manually verified schemes; build partnerships with state governments; have disclaimer about verification

**Risk 2: Users don't trust AI or technology**
- **Mitigation:** Make website functional without AI; work with trusted NGOs and community leaders; show real success stories

**Risk 3: AI gives wrong information**
- **Mitigation:** Always show sources; add disclaimers; human review of AI responses; user feedback mechanism

**Risk 4: Low adoption in rural areas**
- **Mitigation:** Partner with NGOs, Anganwadi workers, Panchayat offices; train community helpers; WhatsApp integration (Phase 3)

**Risk 5: Technical challenges (scale, performance)**
- **Mitigation:** Start small (pilot states), use proven cloud infrastructure, continuous monitoring and optimization

**Risk 6: Sustainability (funding beyond initial phase)**
- **Mitigation:** Demonstrate impact with metrics, apply for government grants, explore CSR partnerships, minimal ongoing costs

---

## 10. Success Stories (What Impact Looks Like)

**Story 1: Farmer Saves Crop**
> "Rajesh, a farmer in Maharashtra, discovered the Pradhan Mantri Fasal Bima Yojana through our platform. He enrolled in crop insurance just weeks before unexpected rains damaged his field. The insurance payout of ₹45,000 saved him from debt."

**Story 2: Girl Goes to College**
> "Priya's family couldn't afford college fees. Through our platform, her mother discovered the Post-Matric Scholarship. Priya received ₹35,000, enrolled in engineering college, and is now on track to become the first college graduate in her family."

**Story 3: Elderly Gets Pension**
> "Ramabai, 68, never knew about the old-age pension scheme. An NGO worker showed her our platform. Within a month, she started receiving ₹1,500/month pension, giving her financial independence."

---

## 11. Why This Project Matters

### 11.1 Social Impact

**Bridging the Information Gap:**
- 400+ million Indians who qualify for schemes but don't know about them
- Estimated ₹2 lakh crore in allocated benefits that go unclaimed every year
- Our platform can help unlock these benefits for the people who need them most

**Empowering the Marginalized:**
- Rural communities with limited access to information
- Women who face mobility constraints
- Semi-literate individuals who struggle with forms
- Regional language speakers excluded by English-only systems

**Strengthening Democracy:**
- Citizens knowing their rights and entitlements
- Government schemes actually reaching intended beneficiaries
- Reducing corruption (less room for middlemen when information is transparent)
- Increasing trust in government programs

### 11.2 Alignment with National Goals

**Digital India:**
- Makes government services accessible digitally
- Supports last-mile digital inclusion
- Leverages technology for social good

**Financial Inclusion:**
- Connects people to government financial schemes
- Reduces poverty through access to benefits
- Supports vulnerable populations

**Ease of Living:**
- Simplifies interaction with government
- Reduces time and effort to access schemes
- Improves quality of life for millions

---

## 12. Next Steps

### 12.1 Immediate Actions (Next 30 Days)

1. **Validate concept with users**
   - Conduct 50+ user interviews in rural/semi-urban areas
   - Test voice interface with target demographic
   - Gather feedback on design mockups

2. **Partnership outreach**
   - Contact 2-3 state governments for data access
   - Reach out to NGOs for pilot partnership
   - Connect with potential funders

3. **Technical validation**
   - Build basic prototype with 10 sample schemes
   - Test AI voice recognition in Hindi/English
   - Verify infrastructure costs




---

## Conclusion

This project addresses a fundamental barrier to social equity in India: **the information gap between government schemes and the people who need them most.**

Our approach is practical, scalable, and focused on real impact:
- ✅ Simple website that works for everyone
- ✅ AI that speaks people's language (literally)
- ✅ Proven technology, realistic budget
- ✅ Clear path from pilot to national scale
- ✅ Measurable social impact

We believe that **information should not be a privilege**. Every Indian who qualifies for a government scheme should know about it, understand if they're eligible, and know exactly how to apply.

This platform makes that possible.

---

## Appendix: Glossary

**Key Terms:**
- **PDS:** Public Distribution System (ration card system)
- **Panchayat:** Local self-government at village level
- **SC/ST/OBC:** Scheduled Caste/Scheduled Tribe/Other Backward Classes
- **CSR:** Corporate Social Responsibility
- **NGO:** Non-Governmental Organization
- **IVR:** Interactive Voice Response (phone-based system)
- **AI:** Artificial Intelligence
- **Voice-first:** Designed primarily for voice interaction (not typing)

---

**Document Version:** 1.0  
**Last Updated:** February 2026  
**Contact:** [Your contact information]

### Primary Users
1. **Rural citizens** - Limited internet access, prefer voice, local language speakers
2. **Semi-urban citizens** - Basic smartphone users, mixed language proficiency
3. **Low-income urban citizens** - Need assistance navigating bureaucracy

### Secondary Users
1. **NGO workers** - Help citizens discover and apply for schemes
2. **Government field workers** - Answer citizen queries
3. **Students/Researchers** - Study scheme effectiveness

### Administrators
1. **Content managers** - Update scheme information (state/central govt officials)
2. **System administrators** - Maintain technical infrastructure
3. **Support team** - Handle user issues and feedback

---

## 4. Functional Requirements

### 4.1 Public Information Portal (Core Website)

#### FR-1: State-wise Scheme Listing
**Priority:** P0 (Must Have)

**Description:** Display all active schemes for each state in India

**Requirements:**
- FR-1.1: System shall display a homepage with all 28 states + 8 UTs listed
- FR-1.2: Each state page shall show all active state government schemes
- FR-1.3: Schemes shall be categorized (Health, Education, Employment, Housing, Food Security, etc.)
- FR-1.4: Users shall be able to filter schemes by category
- FR-1.5: Each scheme shall display:
  - Scheme name (in English + local language)
  - Brief description (100-200 words)
  - Eligibility criteria (simplified)
  - Required documents
  - Application deadline (if applicable)
  - Official application URL
  - Last updated date
- FR-1.6: System shall indicate if a scheme is "Expiring Soon" (within 30 days)
- FR-1.7: System shall mark schemes as "Inactive" rather than deleting them

**Acceptance Criteria:**
- User can navigate from homepage → state → scheme details in ≤3 clicks
- All text is readable without horizontal scrolling on mobile
- Scheme pages load in <3 seconds on 3G

---

#### FR-2: National Scheme Listing
**Priority:** P0 (Must Have)

**Description:** Display all central government schemes available across India

**Requirements:**
- FR-2.1: System shall have a dedicated national schemes section
- FR-2.2: National schemes shall be categorized similarly to state schemes
- FR-2.3: Each national scheme page shall clearly indicate "Available in all states"
- FR-2.4: System shall show state-specific application procedures where applicable
- FR-2.5: Popular national schemes (PM-Kisan, Ayushman Bharat, etc.) shall be featured on homepage

**Acceptance Criteria:**
- User can distinguish between state and national schemes clearly
- National schemes are accessible from any state page
- All major central schemes (50+ schemes) are listed

---

#### FR-3: Multi-language Support
**Priority:** P0 (Must Have - Phase 1: Hindi/English; Phase 2: Regional)

**Description:** Provide content in multiple Indian languages

**Requirements:**
- FR-3.1: System shall support Hindi and English in Phase 1
- FR-3.2: System shall support 6+ regional languages in Phase 2:
  - Tamil, Telugu, Bengali, Marathi, Gujarati, Kannada
- FR-3.3: User shall be able to switch language via dropdown/toggle
- FR-3.4: Language preference shall persist in browser session
- FR-3.5: All UI elements (buttons, labels, headings) shall be translated
- FR-3.6: Scheme content shall be available in at least 2 languages (English + Hindi/Local)
- FR-3.7: If translation is unavailable, system shall indicate "English only" with icon

**Acceptance Criteria:**
- Language switch happens instantly without page reload
- Translation coverage is ≥95% for supported languages
- No broken text or layout issues in any language

---

#### FR-4: Search Functionality
**Priority:** P0 (Must Have)

**Description:** Allow users to search for schemes by keywords

**Requirements:**
- FR-4.1: System shall provide a search bar on every page
- FR-4.2: Search shall work across:
  - Scheme names
  - Descriptions
  - Eligibility criteria
  - Keywords/tags
- FR-4.3: Search shall support both English and local language queries
- FR-4.4: System shall show search suggestions as user types (auto-complete)
- FR-4.5: Search results shall be ranked by relevance
- FR-4.6: Users shall be able to filter results by:
  - State
  - Category
  - Eligibility (age, income, occupation)
- FR-4.7: System shall highlight search terms in results
- FR-4.8: "No results" page shall suggest related schemes or categories

**Acceptance Criteria:**
- Search returns results in <2 seconds
- Top 3 results are relevant to query in 80%+ cases
- Auto-complete suggests relevant schemes

---

#### FR-5: Office Locator
**Priority:** P1 (Should Have)

**Description:** Help users find nearby government offices for applications

**Requirements:**
- FR-5.1: System shall maintain database of government offices:
  - Panchayat offices
  - Municipal offices
  - District offices
  - Specialized offices (Ration, Employment, etc.)
- FR-5.2: Each office listing shall include:
  - Name and type
  - Address
  - Phone number
  - Working hours
  - Map location (lat/long)
- FR-5.3: Users shall be able to search offices by:
  - District/City
  - Office type
  - Proximity (if location shared)
- FR-5.4: Scheme pages shall link to relevant offices
- FR-5.5: System shall integrate with Google Maps for directions

**Acceptance Criteria:**
- Office database covers all districts in pilot states
- Map integration works on mobile browsers
- Contact information is verified and current

---

#### FR-6: Document Checklist
**Priority:** P1 (Should Have)

**Description:** Provide clear lists of required documents for each scheme

**Requirements:**
- FR-6.1: Each scheme shall have a "Required Documents" section
- FR-6.2: Documents shall be listed with:
  - Document name (Aadhaar, Income Certificate, etc.)
  - Purpose (why it's needed)
  - Where to obtain it
- FR-6.3: Common documents shall have dedicated explainer pages:
  - What is it?
  - How to get it?
  - Typical processing time
  - Cost (if any)
- FR-6.4: Users shall be able to generate a printable checklist
- FR-6.5: System shall indicate if documents can be submitted online vs physical

**Acceptance Criteria:**
- Every scheme has complete document list
- Document explainer pages exist for 20+ common documents
- Checklist is printer-friendly

---

### 4.2 AI Assistant Features

#### FR-7: Voice Input
**Priority:** P0 (Must Have)

**Description:** Allow users to interact with the system via voice

**Requirements:**
- FR-7.1: System shall accept voice input via:
  - Microphone (web/mobile)
  - Phone call (IVR - Phase 2)
- FR-7.2: System shall support voice input in Hindi and English (Phase 1)
- FR-7.3: System shall support 6+ regional languages (Phase 2)
- FR-7.4: Voice recording shall have visual feedback (waveform/indicator)
- FR-7.5: Users shall be able to stop/restart recording
- FR-7.6: System shall convert voice to text within 3 seconds
- FR-7.7: System shall display transcription for user verification
- FR-7.8: Users shall be able to edit transcription if incorrect

**Acceptance Criteria:**
- Voice recognition accuracy ≥85% for Hindi/English
- Transcription appears within 3 seconds
- Works in moderate background noise

---

#### FR-8: Voice Output
**Priority:** P0 (Must Have)

**Description:** Provide responses in natural-sounding voice

**Requirements:**
- FR-8.1: System shall convert text responses to speech
- FR-8.2: Voice shall sound natural (not robotic)
- FR-8.3: Voice shall match user's selected language
- FR-8.4: Users shall be able to:
  - Pause/resume audio
  - Adjust playback speed
  - Replay response
- FR-8.5: System shall also display text version simultaneously
- FR-8.6: Audio shall be optimized for low-bandwidth (compressed)

**Acceptance Criteria:**
- Voice quality rated ≥3.5/5 by users
- Audio plays without buffering on 3G
- Text and audio are perfectly synchronized

---

#### FR-9: Intent Recognition
**Priority:** P0 (Must Have)

**Description:** Understand what user is asking for

**Requirements:**
- FR-9.1: System shall identify user intent from natural language input:
  - Finding schemes
  - Checking eligibility
  - Understanding application process
  - Getting document information
  - Finding offices
- FR-9.2: System shall extract key entities:
  - Occupation (farmer, daily wage worker, student, etc.)
  - Age/age group
  - Income level
  - Family composition
  - Location (state, district)
  - Documents they have/need
- FR-9.3: System shall handle ambiguous queries by asking clarifying questions
- FR-9.4: System shall maintain conversation context (remember previous messages)
- FR-9.5: System shall recognize common misspellings and variations

**Acceptance Criteria:**
- Intent correctly identified in 85%+ of queries
- Entity extraction accuracy ≥80%
- Context maintained across 5+ conversation turns

---

#### FR-10: Eligibility Matching
**Priority:** P0 (Must Have)

**Description:** Match users to schemes they qualify for

**Requirements:**
- FR-10.1: System shall compare user profile against scheme eligibility criteria:
  - Age requirements
  - Income limits
  - Occupation
  - Residence (state-specific)
  - Family composition
  - Special conditions (gender, disability, caste, etc.)
- FR-10.2: System shall rank matching schemes by relevance
- FR-10.3: System shall explain why user qualifies ("You match because...")
- FR-10.4: System shall indicate confidence level (Definitely Eligible / Likely / Possibly)
- FR-10.5: If user doesn't match exactly, system shall suggest closest schemes
- FR-10.6: System shall consider both state and national schemes
- FR-10.7: System shall update matches as more user info is collected

**Acceptance Criteria:**
- Top 3 matches are genuinely relevant in 80%+ cases
- Eligibility explanation is clear and accurate
- No false positives (saying user qualifies when they don't)

---

#### FR-11: Step-by-Step Guidance
**Priority:** P0 (Must Have)

**Description:** Guide users through the application process

**Requirements:**
- FR-11.1: For each scheme, system shall provide:
  - Pre-application checklist (what to prepare)
  - Step-by-step instructions (numbered steps)
  - Where to go (office/online)
  - What to say/do at each step
  - Common mistakes to avoid
  - Expected timeline
- FR-11.2: Instructions shall be in simple, conversational language
- FR-11.3: System shall break complex processes into small steps (≤5 steps ideally)
- FR-11.4: Each step shall have:
  - Clear action ("Go to Panchayat office")
  - Required items ("Bring Aadhaar and 2 photos")
  - Expected outcome ("You will receive acknowledgment slip")
- FR-11.5: System shall adapt guidance based on user's location (state-specific procedures)
- FR-11.6: Users shall be able to save/bookmark guidance for later

**Acceptance Criteria:**
- Guidance is complete for top 50 schemes
- Users rate clarity ≥4/5
- Instructions match actual government procedures

---

#### FR-12: Conversation Memory
**Priority:** P1 (Should Have)

**Description:** Remember conversation context within a session

**Requirements:**
- FR-12.1: System shall maintain conversation history for current session
- FR-12.2: Users shall be able to reference previous messages:
  - "What was the second scheme you mentioned?"
  - "Tell me more about that"
- FR-12.3: System shall remember user's stated profile:
  - If user says "I am a farmer" early in conversation, system remembers
- FR-12.4: Session shall persist for 1 hour of inactivity
- FR-12.5: Users shall be able to view conversation history
- FR-12.6: Users shall be able to start fresh conversation (clear context)

**Acceptance Criteria:**
- Context correctly maintained across 10+ turns
- User can resume conversation after 30 min break
- No mixing of conversations across users

---

#### FR-13: Multilingual AI Interaction
**Priority:** P0 (Must Have)

**Description:** AI assistant works in multiple languages

**Requirements:**
- FR-13.1: AI shall understand and respond in:
  - Hindi (Phase 1)
  - English (Phase 1)
  - 6+ regional languages (Phase 2)
- FR-13.2: AI shall detect user's language automatically
- FR-13.3: Users shall be able to switch languages mid-conversation
- FR-13.4: AI shall maintain consistent tone and helpfulness across languages
- FR-13.5: AI shall handle code-mixing (Hinglish, etc.)

**Acceptance Criteria:**
- Language detection accuracy ≥90%
- Response quality consistent across Hindi/English
- Code-mixing handled gracefully

---

### 4.3 Content Management System (CMS)

#### FR-14: Scheme Management
**Priority:** P0 (Must Have)

**Description:** Allow administrators to add/edit schemes

**Requirements:**
- FR-14.1: Admin shall be able to create new scheme entry via form
- FR-14.2: Form shall include fields for:
  - Scheme name (multi-language)
  - Description (multi-language)
  - Category selection (dropdown)
  - State/National selection
  - Eligibility criteria (structured form)
  - Required documents (checkboxes)
  - Application URL
  - Deadline (date picker)
  - Benefits description
- FR-14.3: Admin shall be able to upload supporting documents (PDFs)
- FR-14.4: Admin shall be able to preview scheme page before publishing
- FR-14.5: Admin shall be able to:
  - Save as draft
  - Publish
  - Unpublish (make inactive)
  - Delete
- FR-14.6: System shall maintain version history
- FR-14.7: System shall show who created/edited each scheme and when

**Acceptance Criteria:**
- Non-technical user can add scheme in <10 minutes
- Form validation prevents incomplete entries
- All changes are logged

---

#### FR-15: Bulk Import
**Priority:** P1 (Should Have)

**Description:** Allow bulk upload of scheme data

**Requirements:**
- FR-15.1: Admin shall be able to upload CSV/Excel file
- FR-15.2: System shall provide template file for download
- FR-15.3: System shall validate uploaded data:
  - Required fields present
  - Correct data types
  - No duplicates
- FR-15.4: System shall show import preview before confirming
- FR-15.5: System shall report errors with line numbers
- FR-15.6: Admin shall be able to fix errors and re-upload

**Acceptance Criteria:**
- Successfully import 100+ schemes in <5 minutes
- Error reporting is clear and actionable
- No data corruption

---

#### FR-16: Office Management
**Priority:** P1 (Should Have)

**Description:** Manage government office database

**Requirements:**
- FR-16.1: Admin shall be able to add/edit office information
- FR-16.2: Form shall include:
  - Office name
  - Type (Panchayat, Municipal, etc.)
  - State, District, City
  - Address
  - Contact details
  - Working hours
  - Map coordinates (auto-populated from address)
- FR-16.3: Admin shall be able to link offices to relevant schemes
- FR-16.4: System shall verify address using Google Maps API
- FR-16.5: Admin shall be able to bulk import offices via CSV

**Acceptance Criteria:**
- Office database has ≥500 entries for pilot states
- Map integration is accurate
- Contact info is current

---

#### FR-17: User Role Management
**Priority:** P1 (Should Have)

**Description:** Different permission levels for admins

**Requirements:**
- FR-17.1: System shall support roles:
  - Super Admin (full access)
  - State Admin (can edit only their state's schemes)
  - Content Editor (can create/edit but not publish)
  - Viewer (read-only)
- FR-17.2: Each role shall have clearly defined permissions
- FR-17.3: Super Admin shall be able to create/delete user accounts
- FR-17.4: Super Admin shall be able to assign/change roles
- FR-17.5: System shall log all admin actions

**Acceptance Criteria:**
- Permissions are enforced correctly
- State Admins cannot edit other states' content
- Audit log is complete

---

### 4.4 Analytics & Reporting

#### FR-18: Usage Analytics
**Priority:** P1 (Should Have)

**Description:** Track how users interact with the system

**Requirements:**
- FR-18.1: System shall track:
  - Daily/monthly active users
  - Page views per scheme
  - Search queries
  - Most viewed schemes
  - State-wise usage
  - Language preferences
  - Device types (mobile/desktop)
  - Conversation length (AI assistant)
- FR-18.2: Admin dashboard shall display:
  - Real-time user count
  - Top 10 schemes this week
  - Search trends
  - Geographic distribution
- FR-18.3: System shall generate weekly/monthly reports
- FR-18.4: Reports shall be exportable as PDF/CSV
- FR-18.5: System shall track conversion funnel:
  - Scheme discovered → Eligibility checked → Clicked application link

**Acceptance Criteria:**
- Dashboard loads in <3 seconds
- Data is accurate and real-time
- Reports are automatically generated

---

#### FR-19: AI Performance Metrics
**Priority:** P1 (Should Have)

**Description:** Monitor AI assistant effectiveness

**Requirements:**
- FR-19.1: System shall track:
  - Total conversations
  - Average conversation length
  - Intent recognition accuracy
  - Entity extraction accuracy
  - User satisfaction (thumbs up/down after each response)
  - Schemes recommended vs schemes clicked
  - Voice recognition error rate
- FR-19.2: System shall flag low-quality interactions for review
- FR-19.3: System shall identify common user questions not answered well
- FR-19.4: Admin shall be able to see conversation transcripts (anonymized)

**Acceptance Criteria:**
- All metrics update hourly
- Accuracy metrics are ≥85%
- Satisfaction rate ≥75%

---

#### FR-20: Feedback Collection
**Priority:** P1 (Should Have)

**Description:** Gather user feedback

**Requirements:**
- FR-20.1: Users shall be able to rate each AI response (thumbs up/down)
- FR-20.2: Users shall be able to submit feedback form:
  - What worked well?
  - What didn't work?
  - Suggestions
- FR-20.3: Users shall be able to report incorrect information
- FR-20.4: Feedback shall be visible in admin dashboard
- FR-20.5: System shall send email notification for critical feedback

**Acceptance Criteria:**
- Feedback form is simple (<5 fields)
- ≥10% of users provide feedback
- All feedback is reviewed weekly

---

## 5. Non-Functional Requirements

### 5.1 Performance

#### NFR-1: Response Time
- Web pages shall load in <3 seconds on 3G networks
- Search results shall appear in <2 seconds
- Voice transcription shall complete in <3 seconds
- AI responses shall start streaming in <2 seconds

#### NFR-2: Throughput
- System shall handle 10,000 concurrent users (Phase 1)
- System shall handle 100,000 concurrent users (Phase 3)
- API shall process 1,000 requests/second

#### NFR-3: Scalability
- System architecture shall support horizontal scaling
- Database shall support read replicas
- Static content shall be served via CDN

---

### 5.2 Availability & Reliability

#### NFR-4: Uptime
- System shall maintain 99.5% uptime (Phase 1)
- System shall maintain 99.9% uptime (Phase 3)
- Scheduled maintenance shall be announced 48 hours in advance

#### NFR-5: Disaster Recovery
- Database backups shall be taken every 6 hours
- System shall support point-in-time recovery
- Recovery Time Objective (RTO): 4 hours
- Recovery Point Objective (RPO): 6 hours

#### NFR-6: Fault Tolerance
- Website shall function even if AI service is down
- Cached content shall be served if database is unavailable
- Graceful degradation for all features

---

### 5.3 Security & Privacy

#### NFR-7: Data Privacy
- System shall NOT store user voice recordings permanently
- User interactions shall be anonymized for analytics
- No Personally Identifiable Information (PII) shall be collected without consent
- System shall comply with IT Act 2000

#### NFR-8: Authentication & Authorization
- Admin panel shall require username/password authentication
- Passwords shall be hashed using bcrypt or Argon2
- Session timeout after 30 minutes of inactivity
- Failed login attempts shall be rate-limited

#### NFR-9: Data Security
- All traffic shall use HTTPS (TLS 1.3)
- Database shall encrypt data at rest
- API keys shall be rotated every 90 days
- No sensitive data in logs

#### NFR-10: Input Validation
- All user inputs shall be sanitized to prevent:
  - SQL injection
  - XSS attacks
  - CSRF attacks
- File uploads shall be scanned for malware

---

### 5.4 Usability

#### NFR-11: Accessibility
- Website shall meet WCAG 2.1 Level AA standards
- All images shall have alt text
- Keyboard navigation shall be fully supported
- Color contrast ratio shall be ≥4.5:1
- Screen reader compatible

#### NFR-12: Mobile Responsiveness
- Website shall work on screen sizes from 320px to 2560px
- Touch targets shall be ≥44x44 pixels
- Forms shall be easy to fill on mobile
- No horizontal scrolling required

#### NFR-13: Browser Compatibility
- Support for:
  - Chrome 90+
  - Firefox 88+
  - Safari 14+
  - Edge 90+
  - Chrome Mobile (Android)
  - Safari Mobile (iOS)

#### NFR-14: User Experience
- Navigation shall be intuitive (≤3 clicks to any page)
- Error messages shall be helpful, not technical
- Loading states shall have clear indicators
- Success/failure feedback for all actions

---

### 5.5 Maintainability

#### NFR-15: Code Quality
- Code shall follow industry standard conventions
- Code coverage shall be ≥70% for critical paths
- All functions shall have documentation
- Code shall pass linting checks

#### NFR-16: Logging & Monitoring
- All errors shall be logged with stack traces
- API requests shall be logged
- Performance metrics shall be collected
- Alerts for critical failures

#### NFR-17: Documentation
- API documentation shall be auto-generated (OpenAPI/Swagger)
- Admin user guide shall be maintained
- Deployment procedures shall be documented
- Database schema shall be documented

---

### 5.6 Localization & Internationalization

#### NFR-18: Language Support
- UI shall support right-to-left languages (future: Urdu)
- Date/time formats shall follow local conventions
- Number formats shall use Indian numbering system (lakhs, crores)
- Currency shall be displayed as ₹

#### NFR-19: Character Encoding
- All text shall use UTF-8 encoding
- System shall support Unicode characters for all Indian languages
- No garbled text in any supported language

---

### 5.7 Compliance & Legal

#### NFR-20: Accessibility Compliance
- Comply with Rights of Persons with Disabilities Act 2016
- Provide alternative text for all visual content
- Support keyboard-only navigation

#### NFR-21: Data Retention
- Conversation logs shall be retained for 90 days (anonymized)
- Analytics data shall be retained for 2 years
- Inactive user accounts shall be deleted after 1 year

#### NFR-22: Content Accuracy
- All scheme information shall be verified against official sources
- Outdated schemes shall be marked as inactive within 7 days
- Disclaimer shall state "Information is for reference only; verify with official sources"

---

## 6. Constraints

### Technical Constraints
- Must work on low-end Android devices (2GB RAM)
- Must function on 2G/3G networks (not just 4G/5G)
- Budget limit of $3,000/month for Phase 1 infrastructure
- Must use existing government APIs where available

### Business Constraints
- Launch pilot within 3 months
- Must obtain scheme data from state governments (cooperation required)
- Cannot guarantee real-time updates (government data update frequency varies)

### Regulatory Constraints
- Must not store sensitive user data without consent
- Must comply with IT Act 2000
- Cannot guarantee eligibility (only provide information)
- Must include disclaimers about official verification

---

## 7. Assumptions

1. State governments will provide/approve accurate scheme data
2. Users have basic smartphone or feature phone with internet
3. Majority of target users speak Hindi or regional language (limited English)
4. Users may have limited digital literacy
5. Internet connectivity may be intermittent
6. Government office contact information is publicly available

---

## 8. Dependencies

### External Dependencies
- Google Cloud Speech-to-Text API
- Google Cloud Text-to-Speech API
- Claude/GPT-4 API availability
- Google Maps API
- Government websites for official scheme data

### Internal Dependencies
- Content team to populate scheme database
- Partnership with state governments for data access
- User testing participants for feedback
- Marketing team for user acquisition

---

## 9. Future Enhancements (Out of Scope for Phase 1)

### Phase 2 Features
- WhatsApp bot integration
- SMS-based interaction (for users without internet)
- Application status tracking
- Document upload and verification
- Integration with DigiLocker

### Phase 3 Features
- IVR (phone call-based voice assistant)
- Offline mobile app
- Community forum (users help each other)
- Success stories section
- Gamification (badges for helping others)

---

## 10. Acceptance Criteria Summary

The system shall be considered ready for launch when:

1. ✅ At least 100 schemes populated (50+ per pilot state)
2. ✅ Website loads in <3 seconds on 3G
3. ✅ AI assistant responds correctly to 20 test scenarios
4. ✅ Voice recognition accuracy ≥85% for Hindi/English
5. ✅ Search returns relevant results in 80%+ cases
6. ✅ Mobile responsive on all major devices
7. ✅ Accessibility audit passes with ≥90% score
8. ✅ User testing with 50+ people shows ≥75% satisfaction
9. ✅ All P0 and P1 requirements implemented
10. ✅ Security audit completed with no critical issues

---

## 11. Prioritization

### Phase 1 (Pilot - 3 months)
**Must Have (P0):**
- FR-1, FR-2, FR-3, FR-4 (Website with search)
- FR-7, FR-8, FR-9, FR-10, FR-11 (AI assistant basics)
- FR-14 (CMS for scheme management)

**Should Have (P1):**
- FR-5 (Office locator)
- FR-6 (Document checklist)
- FR-18, FR-19, FR-20 (Analytics)

### Phase 2 (Regional Expansion - 6 months)
- Complete P1 features from Phase 1
- FR-12, FR-13 (Enhanced AI features)
- FR-15, FR-16, FR-17 (Complete CMS)
- 6 regional languages

### Phase 3 (National Scale - 12 months)
- All remaining features
- WhatsApp/SMS integration
- IVR system
- Advanced analytics

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | Feb 2026 | Team | Initial requirements |

**Approval:**
- Product Owner: _____________
- Technical Lead: _____________
- Stakeholder: _____________

---

## Appendix A: Glossary

- **PDS**: Public Distribution System (ration system)
- **IVR**: Interactive Voice Response (phone-based system)
- **NLP**: Natural Language Processing
- **STT**: Speech-to-Text
- **TTS**: Text-to-Speech
- **CMS**: Content Management System
- **SSR**: Server-Side Rendering
- **CDN**: Content Delivery Network

---

## Appendix B: Sample Use Cases

### Use Case 1: Farmer Discovers Crop Insurance
**Actor:** Rural farmer with basic smartphone  
**Goal:** Find and apply for crop insurance scheme  
**Precondition:** User has internet access

**Flow:**
1. User opens website
2. Clicks on their state (Maharashtra)
3. Sees category "Agriculture"
4. Finds "Pradhan Mantri Fasal Bima Yojana"
5. Reads eligibility (owns farmland, has Kisan Credit Card)
6. Checks required documents
7. Clicks "Apply Now" → redirected to official portal
8. User can also ask AI: "Mujhe fasal bima chahiye" and get guided through same process

### Use Case 2: Student Finds Scholarship via Voice
**Actor:** High school girl from low-income family  
**Goal:** Find scholarship for higher education  
**Precondition:** User has microphone access

**Flow:**
1. User clicks microphone icon
2. Says in Hindi: "Main 12th pass kar chuki hoon, mujhe scholarship chahiye"
3. AI extracts: student, female, completed 12th
4. AI asks: "Aapke marks kitne hain?" (What are your marks?)
5. User responds: "75%"
6. AI shows 3 relevant scholarships
7. AI explains each in simple language
8. Provides step-by-step application guide

---

**END OF REQUIREMENTS DOCUMENT**
