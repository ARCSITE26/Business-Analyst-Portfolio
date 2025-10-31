# FinServe Bank — Loan Approval Automation
## Business Requirements Document (BRD)

---

## EXECUTIVE SUMMARY

**Project Name:** Loan Processing Automation & Speed Optimization  
**Company:** FinServe Bank (Mid-sized private bank, ~50 lakh retail customers)  
**Document Date:** October 2025  
**Version:** 1.0

### Business Problem

FinServe's retail loan approval process takes **25-30 days**, while competitors (HDFC, ICICI, Lending Kart) approve in **3-5 days**. This is causing:

- **Customer frustration:** 40% of applicants abandon the process
- **Revenue loss:** ₹50 crores annually in lost loan portfolio
- **Competitive disadvantage:** Customers migrate to faster competitors
- **High operational cost:** 200+ staff dedicated to manual processing
- **Compliance risk:** Manual steps bypass regulatory checks

### Business Objective

Reduce loan approval time from 25-30 days to **7 days** while maintaining compliance standards and improving customer experience.

### Expected Business Impact

**12-Month Horizon:**
- Phase 1 (M1-M3): 25 days → 15 days | Recovery: ₹15-20 crores
- Phase 2 (M4-M6): 15 days → 10 days | Recovery: ₹35-40 crores  
- Phase 3 (M7-M12): 10 days → 7 days | Recovery: ₹50 crores
- **Total annual recovery: ₹147 crores**
- **ROI: 210% in Year 1**

---

## CURRENT STATE ANALYSIS (AS-IS)

### Loan Approval Process (25-30 Days — WATERFALL)

| **Stage** | **Duration** | **Process Owner** | **Activities** | **Bottleneck** |
|---|---|---|---|---|
| **Application Submission** | Day 0 | Customer | Online form + document upload | — |
| **Document Verification** | Days 1-3 | Verification Team | Manual check: PAN, Aadhaar, salary slips, bank statements | 🔴 Manual, email-based |
| **Credit Bureau Check** | Days 2-4 | Credit Team | CIBIL score pull, credit history review (MANUAL API CALL) | 🔴 Takes 2 days for 30-min task |
| **Income Verification** | Days 5-8 | Verification Officer | Call customer, verify employment with employer HR | 🔴 Officer availability, phone tag |
| **Underwriting & Decision** | Days 9-15 | Credit Manager | Review all data, apply risk rules, approve/reject | 🔴 Manager handles 50+ apps, bottleneck |
| **Compliance Review** | Days 16-20 | Compliance Officer | Check AML/KYC, regulatory requirements | ⚠️ **DONE AT END → Rework if issues** |
| **Loan Disbursement Setup** | Days 21-25 | Operations Team | Create loan account, generate offer letter | 🔴 Legacy system integration issues |
| **Final Approval & Disbursement** | Days 26-30 | Senior Manager | Sign-off, transfer funds to account | 🔴 Approval bottleneck |

**Critical Finding:** Process is **sequential (waterfall) instead of parallel**. Each step waits for previous one. Compliance check at END causes rework.

### Root Causes Identified

| **Root Cause** | **Impact** | **Why** |
|---|---|---|
| **Manual document verification** | 2 days wasted | No OCR automation |
| **Manual CIBIL checks** | 2 days wasted | No API integration |
| **Compliance at end** | 4 days + rework | Process design flaw |
| **Phone-based income verification** | 3+ days | No video/automated options |
| **Sequential process** | 10+ days unnecessary | Legacy workflow design |
| **Senior manager approval bottleneck** | 4 days | No batch/dashboard approval |

---

## TECHNICAL CONSTRAINTS (From CTO)

| **Component** | **Current State** | **Issue** | **Complexity to Fix** |
|---|---|---|---|
| **Order Management System (OMS)** | 10-year-old Java monolith | Slow, can't handle peak load | HIGH (6-12 months) |
| **Database** | Single MySQL server | Bottleneck during peak load | MEDIUM (4-6 months) |
| **Document Processing** | Manual (humans reading PDFs) | No automation, error-prone | LOW (1-2 months, use AWS Textract) |
| **Credit Bureau Integration** | Manual (log in, download reports) | No API, slow | LOW (1-2 months, integrate CIBIL API) |
| **Video KYC** | Not available | Need platform for remote verification | MEDIUM (2-3 months) |
| **Compliance Automation** | Manual spreadsheet review | No rules engine | MEDIUM (2-3 months) |
| **API Gateway** | Doesn't exist | Can't expose services | MEDIUM (3-4 months) |

---

## STAKEHOLDER ANALYSIS

| **Stakeholder** | **Priority** | **Concern** | **Resistance Risk** |
|---|---|---|---|
| **CEO/MD** | Speed + Revenue | Can we deliver without quality loss? | LOW (revenue-focused) |
| **CTO** | Stability + Maintainability | System will break if we rush | HIGH (defensive about platform) |
| **Chief Risk Officer** | No defaults/losses | Faster approval = more bad loans? | MEDIUM (risk-averse) |
| **Compliance Officer** | Regulatory adherence | Automation skips required checks? | MEDIUM-HIGH (non-negotiable) |
| **Verification Team** | Job security | Will automation eliminate our jobs? | MEDIUM-HIGH (resistance likely) |
| **CFO** | ROI + Cost Control | Investment justified? | LOW (if numbers prove it) |

---

## PROPOSED SOLUTION (TO-BE STATE)

### New Loan Approval Process (7 Days — PARALLEL + AUTOMATION)

**Day 0:** Customer submits application  
↓  
**Day 1:** PARALLEL PROCESSING (All 3 happen simultaneously)
- **Track A:** Document verification (OCR + video call) → ✅ Done
- **Track B:** Credit bureau check (API instant) → ✅ Done  
- **Track C:** Income verification (video call) → ✅ Done

**Day 2:** Compliance automation (AML screening, regulatory check)  
**Days 3-5:** Underwriting (credit manager reviews borderline cases only, AI auto-approves low-risk)  
**Day 6:** Loan account creation (automated) + offer letter generation  
**Day 7:** Senior manager batch approval + fund transfer

**Key Improvements:**
1. **Parallel instead of sequential** → Saves 10+ days
2. **Compliance moved earlier** → No rework
3. **Automation removes manual checks** → 80% auto-approved, 20% manual review
4. **Video KYC for income verification** → Fast, reliable
5. **API-based credit checks** → Instant (previously 2-4 days)

---

## IMPLEMENTATION ROADMAP

### Phase 1: Quick Wins (M1-M3, Target: 15-Day Approval)

**Deliverables:**
1. Document OCR (AWS Textract) + API integration
2. CIBIL credit bureau API integration
3. Video KYC platform (on-call verification)
4. Compliance automation (basic AML rules)

**Investment:** ₹30-40 lakhs  
**Expected improvement:** 25 days → 15 days (40% faster)  
**Revenue recovery:** ₹15-20 crores annually

---

### Phase 2: Process Redesign (M4-M6, Target: 10-Day Approval)

**Deliverables:**
1. Parallel processing workflow (document + credit + income simultaneously)
2. Database optimization + caching
3. Rule-based underwriting (auto-approve <50% of applications)
4. Compliance dashboard (flag-based review)

**Investment:** ₹60-80 lakhs (cumulative ₹1.2 crores)  
**Expected improvement:** 15 days → 10 days (67% faster than baseline)  
**Revenue recovery:** ₹35-40 crores annually

---

### Phase 3: Full Automation (M7-M12, Target: 7-Day Approval)

**Deliverables:**
1. Complete OMS rebuild (modern cloud architecture)
2. AI credit scoring model
3. End-to-end digital workflow
4. Senior manager dashboard (batch approvals)

**Investment:** ₹1 crore (cumulative ₹2.2 crores)  
**Expected improvement:** 10 days → 7 days (77% faster than baseline)  
**Revenue recovery:** ₹50 crores annually

**Total 12-month revenue recovery: ₹147 crores | ROI: 210%**

---

## RISK MITIGATION

| **Risk** | **Mitigation** |
|---|---|
| **Automation approves bad loans** | Keep 20% manual review for borderline cases; use tested ML model |
| **SEBI compliance violation** | Run compliance checks Day 2, not Day 16; audit every auto-approval |
| **Verification team job loss** | Redeploy to video KYC roles (higher-skilled work); no layoffs in Phase 1 |
| **System unstable during rebuild** | Phase approach; prove stability in Phase 1 before Phase 2 |

---

## APPROVAL SIGN-OFF

- ☐ CEO: Approved
- ☐ CTO: Approved  
- ☐ Chief Risk Officer: Approved
- ☐ CFO: Approved

---

*Document Version: 1.0 | Last Updated: October 2025*
