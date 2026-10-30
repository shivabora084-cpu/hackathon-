# LinguaMate AI - Testing Guide

## 1. Automated Integration Tests
The project contains an automated integration test suite validating all primary backend capabilities:
- Platform health check (`GET /api/health`)
- Speech provider capabilities (`GET /api/speech/capabilities`)
- User registration & JWT generation (`POST /api/auth/register`)
- Profile retrieval (`GET /api/auth/me`)
- Contextual idiom translation (`POST /api/translation/translate`)
- Ambiguity & clarification detection (`POST /api/chat/message`)
- Mixed-language parsing (`POST /api/chat/message`)
- Multi-turn pronoun reference resolution (`POST /api/chat/message`)

### Running the automated suite:
```bash
cd backend
npm test
```
Expected output:
```
====================================================
 LinguaMate AI - Automated Integration Verification
 Target URL: http://localhost:5000/api
====================================================

• Testing: GET /api/health responds with status and integration health... ✓ PASSED
• Testing: GET /api/speech/capabilities returns provider configuration... ✓ PASSED
• Testing: POST /api/auth/register creates user and returns JWT... ✓ PASSED
• Testing: GET /api/auth/me returns authenticated user details... ✓ PASSED
• Testing: POST /api/translation/translate translates and explains cultural idiom... ✓ PASSED
• Testing: POST /api/chat/message identifies ambiguity and triggers clarification... ✓ PASSED
• Testing: POST /api/chat/message processes mixed-language inquiry... ✓ PASSED
• Testing: POST /api/chat/message resolves pronoun reference in follow-up... ✓ PASSED

====================================================
 Test Summary: 8 Passed, 0 Failed
====================================================
```

---

## 2. Frontend Production Build Verification
To ensure all React components, context providers, and Tailwind styles compile without errors:
```bash
cd frontend
npm run build
```
Expected output:
```
✓ 1659 modules transformed.
✓ built in ~5s
dist/index.html
dist/assets/index.css
dist/assets/index.js
```

---

## 3. Manual Live Demonstration Tests

### Demo 1: Mixed-Language Understanding
- Navigate to `/app/chat`
- Speak or type: *"Sir, admission fees evlo? Installments-la pay panlama?"*
- **Verify**: The assistant identifies Tanglish (`ta + en`), understands the inquiry, and replies accurately in Tamil or English.

### Demo 2: Contextual Pronoun Memory
- Turn 1: *"What is the admission fee?"*
- Turn 2: *"Can I pay it in installments?"*
- **Verify**: The assistant resolves *"it"* as referring to the admission fee.

### Demo 3: Intelligent Clarification
- Type: *"Cancel it."*
- **Verify**: The assistant displays a clarification card with selectable buttons (e.g. *Academic Service*, *Account Settings*, *Billing / Fees*).

### Demo 4: Two-Person Translation Mode
- Navigate to `/app/dual-translation`
- Set Speaker 1 to English and Speaker 2 to Tamil
- Speak into Speaker 1's microphone → Observe translation synthesized in Tamil for Speaker 2.

### Demo 5: PDF Knowledge Base (RAG)
- Navigate to `/app/knowledge`
- Upload a sample PDF document
- In the Query Sandbox, ask a question based on the PDF
- **Verify**: The assistant responds with the verified answer and cites the source file.
