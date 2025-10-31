# TrendCart E-Commerce Platform
## Business Requirements Document (BRD)

---

## EXECUTIVE SUMMARY

**Project Name:** Cart Abandonment Reduction Program  
**Company:** TrendCart (Mid-size e-commerce platform)  
**Document Date:** October 2025  
**Version:** 1.0  
**Stakeholders:** CEO, CTO, Product Manager, UI/UX Lead, Marketing Lead, Customer Support Manager

### Business Problem

TrendCart currently experiences a **45% cart abandonment rate**, significantly above the industry benchmark of 25-30%. This translates to:
- **Monthly revenue loss:** ₹73.8 lakhs
- **Annual revenue loss:** ₹8.8 crores
- **Customer impact:** 40% of loan applicants abandon the checkout process
- **Competitive disadvantage:** Customers migrate to faster competitors

### Business Objective

Reduce cart abandonment from 45% to 35% within 90 days by addressing:
1. Hidden shipping cost surprises (32% of abandonments)
2. Slow order execution (28% of abandonments)
3. Mobile platform friction (15% vs 35% desktop conversion rate)

### Expected Business Impact

**3-Month Horizon:**
- Phase 1 quick wins: ₹34 lakhs monthly recovery
- Phase 2 mobile optimization: ₹30-40 lakhs additional
- **Total 90-day recovery: ₹64-74 lakhs**
- **ROI: 1,133% (Phase 1 alone)**

---

## CURRENT STATE ANALYSIS (AS-IS)

### 2.1 Checkout Funnel Breakdown

| **Stage** | **Users** | **% Complete** | **% Abandonment** | **Key Issues** |
|---|---|---|---|---|
| Add to Cart | 10,000 | 100% | — | — |
| Proceed to Checkout | 7,000 | 70% | 30% | Users leaving pre-checkout |
| Reach Payment Page | 4,200 | 42% | 58% | **Hidden shipping costs revealed** |
| Complete Payment | 2,310 | 23.1% | 77% | **Payment friction, unexpected charges** |

**Critical Finding:** The biggest drop-off (45%) occurs at payment stage, costing ₹45 lakhs in monthly revenue.

### 2.2 Platform Performance Comparison

| **Metric** | **Desktop** | **Mobile** | **Gap** | **Impact** |
|---|---|---|---|---|
| Traffic Volume | 40% (4,000 users) | 60% (6,000 users) | — | Mobile is primary channel |
| Completion Rate | 35% | 15% | **20 percentage points** | **Losing ₹25-30 lakhs/month on mobile** |
| Page Load Time | 1.8s | 3.2s | 1.4s slower | Mobile users frustrated |

### 2.3 Customer Complaint Analysis (Last 30 Days: 127 total)

| **Complaint Category** | **Count** | **%** | **Impact** |
|---|---|---|---|
| "Payment not going through" | 45 | 35% | Direct revenue loss |
| "Hidden/unexpected charges" | 32 | 25% | Trust loss, abandonment |
| "Forgot password during checkout" | 28 | 22% | Friction in authentication |
| "Too many checkout steps" | 22 | 17% | Complexity discourages users |

### 2.4 Customer Survey Data (100 Abandoned Users)

| **Reason for Abandonment** | **%** | **User Impact** |
|---|---|---|
| Unexpected charges/hidden costs | 35% | ~2,240 users/month |
| Too many steps | 28% | ~1,960 users/month |
| Payment issues/failures | 22% | ~1,400 users/month |
| Trust/security concerns | 15% | ~1,050 users/month |

---

## ROOT CAUSE ANALYSIS

### 3.1 Problem: Hidden Shipping Charges (32% of abandonments)

**Why It Happens:**
- Shipping cost displays only at final checkout stage
- Customers see total price for first time → Sticker shock
- No upfront estimation on product or cart page

**Business Impact:** ₹20-25 lakhs monthly lost revenue  
**Frequency:** 2,240 users/month  
**Severity:** HIGH (easy to fix, high impact)

---

### 3.2 Problem: Slow Payment Processing (28% of abandonments)

**Why It Happens:**
- Checkout page load time: 2-3 seconds (should be <1s)
- Order processing: Multiple validation steps
- No real-time feedback on payment status

**Business Impact:** ₹25-30 lakhs monthly lost revenue  
**Frequency:** 1,960 users/month  
**Severity:** CRITICAL (affects conversion directly)

---

### 3.3 Problem: Mobile Platform Friction (15% conversion vs 35% desktop)

**Why It Happens:**
- Form fields not optimized for mobile
- 5-step checkout process (should be 3 steps)
- Keyboard input repeatedly required
- Images not optimized (slow load on 4G)

**Business Impact:** ₹25-30 lakhs monthly lost revenue  
**Frequency:** 6,000 mobile users/month  
**Severity:** CRITICAL (majority of traffic)

---

## STAKEHOLDER ANALYSIS

| **Stakeholder** | **Role** | **Key Priorities** | **Concerns** | **Win For Them** |
|---|---|---|---|---|
| **CEO** | Decision Maker | Revenue growth, quick wins | Time to implement, ROI proof | Visible improvement in 2-3 months |
| **CTO** | Technology Owner | System stability, not blamed | Told to rush; fears stability impact | Data showing fixes won't break platform |
| **Product Manager** | Product Owner | User satisfaction | Conflicting feature demands | Prioritized roadmap |
| **UI/UX Lead** | Design Owner | Design quality, not blamed | Accused of "bad UX" | Data showing UX is secondary issue |
| **Marketing Lead** | Demand Gen | Conversion rates | Doesn't want to blame traffic quality | Proof it's not a "bad leads" problem |
| **Support Manager** | Customer Voice | Fewer complaints | Overwhelmed with tickets | Clear solution + training |

### Stakeholder Conflicts & Navigation

**Conflict #1: Marketing vs CTO**
- Marketing: "Bad traffic quality → low conversion"
- CTO: "Bad platform → high abandonment"
- **Reality:** Both partially right. Mobile UX + hidden charges = primary issues
- **Resolution:** Phase approach—fix platform first, then optimize traffic

**Conflict #2: CEO vs CTO**
- CEO: "We need results in 2 months"
- CTO: "Proper fixes need 3 months minimum"
- **Resolution:** Quick wins (UPI, shipping display) in 2 months + mobile optimization in months 3-4

---

## SOLUTION DESIGN (TO-BE STATE)

### 4.1 Phase 1: Quick Wins (0-2 Weeks) — Focus: Immediate Revenue Recovery

#### **Requirement 1.1: Display Shipping Charges Upfront**

**User Story:**
> As a customer, I want to see shipping costs on the product page and in my cart, so I know the final price before checkout.

**Acceptance Criteria:**
- ✅ Shipping cost visible on product detail page (below price)
- ✅ Shipping cost visible on cart summary (before "Proceed to Checkout")
- ✅ Cost is dynamic based on postal code (if applicable)
- ✅ Mobile version displays clearly (not cut off)
- ✅ Estimated delivery date shown alongside cost

**Business Impact:**
- Reduces complaints: 32 tickets/month → 5 tickets/month
- Expected recovery: ₹20-25 lakhs/month
- Users informed = reduced surprises = higher confidence

**Effort:** 2-3 days (frontend only, no backend changes)  
**Owner:** Frontend Developer + UI Designer  
**Priority:** CRITICAL

---

#### **Requirement 1.2: Exit-Intent Discount Popup**

**User Story:**
> As a business, I want to show a discount offer when customers try to leave checkout, so I can recover abandoned transactions.

**Acceptance Criteria:**
- ✅ Popup triggers when user moves mouse toward browser close button
- ✅ Offers 5% discount code (valid 24 hours)
- ✅ NOT shown on mobile (too intrusive)
- ✅ "No Thanks" button closes without obstruction
- ✅ Discount applies to cart total (including shipping)

**Business Impact:**
- Expected recovery: 10-15% of abandoning users = ₹7-11 lakhs/month
- CTR target: ≥10%

**Effort:** 3-5 days  
**Owner:** Frontend Developer + Marketing  
**Priority:** HIGH

---

#### **Requirement 1.3: WhatsApp Abandoned Cart Reminders**

**User Story:**
> As a business, I want to send WhatsApp reminders to customers with abandoned carts, so I can re-engage them cost-effectively.

**Acceptance Criteria:**
- ✅ Message sent 2 hours after cart abandonment
- ✅ Includes: Product name, price, direct checkout link, 10% discount code
- ✅ Customers can opt out
- ✅ Follow-up message sent 24 hours later if first not clicked
- ✅ Delivery + click-through tracked

**Business Impact:**
- Expected recovery: 8-12% of abandoned carts = ₹6-9 lakhs/month
- Industry benchmark: 8-12% recovery rate

**Effort:** 1 week (WhatsApp Business API integration)  
**Owner:** Marketing + Backend Developer  
**Priority:** HIGH

---

### 4.2 Phase 2: Mobile Optimization (Weeks 3-6) — Focus: Platform Experience

#### **Requirement 2.1: Simplified Mobile Checkout**

**User Story:**
> As a mobile user, I want to complete checkout in 3 steps with minimal typing, so I can quickly purchase without frustration.

**Acceptance Criteria:**
- ✅ Reduce from 5 steps to 3: (1) Shipping, (2) Payment, (3) Confirmation
- ✅ Auto-fill customer data (address, payment method from profile)
- ✅ Single-page checkout (scroll instead of multiple pages)
- ✅ Form validation inline (real-time error messages)
- ✅ Page load time <2 seconds on 4G networks
- ✅ Mobile conversion: Target increase from 15% to 30%

**Business Impact:**
- Expected recovery: ₹30-40 lakhs/month additional
- ARPU increase (more orders placed)

**Effort:** 4-6 weeks  
**Owner:** Product Manager + Mobile Development Team  
**Priority:** CRITICAL

---

#### **Requirement 2.2: One-Click Payment (Mobile)**

**User Story:**
> As a returning mobile user, I want to pay with saved card/UPI in one click, so I don't re-enter details every time.

**Acceptance Criteria:**
- ✅ "Save card for future purchases" enabled by default
- ✅ Show last 4 digits + expiry for saved cards
- ✅ One-click checkout completes in <5 seconds
- ✅ Option to change payment method before final confirmation

**Business Impact:**
- Faster checkout = higher completion rates
- Reduces payment friction significantly

**Effort:** 2-3 weeks  
**Owner:** Payment Integration Team  
**Priority:** HIGH

---

### 4.3 Phase 3: Long-Term Strategic Improvements (Months 2-3)

- **Guest checkout** (no forced login) → Reduces friction for first-time buyers
- **Trust signals** (SSL badges, "100% secure," guarantees) → Addresses 15% with trust concerns
- **Advanced payment options** (BNPL: ZestMoney, Simpl) → Increases basket size

---

## IMPLEMENTATION ROADMAP

### Phase 1 Timeline (0-2 Weeks)

| **Week** | **Task** | **Owner** | **Deliverable** |
|---|---|---|---|
| **Week 1** | - Implement shipping display<br>- Build exit-intent popup<br>- WhatsApp API setup | Frontend Dev + Marketing | 3 features live |
| **Week 2** | - Full QA across devices<br>- Monitor support tickets<br>- Track popup interactions | QA Team | Performance metrics |

**Phase 1 Impact:** Revenue +₹34 lakhs/month

---

### Phase 2 Timeline (Weeks 3-6)

| **Week** | **Task** | **Owner** | **Deliverable** |
|---|---|---|---|
| **Week 3-4** | Mobile checkout redesign (mockups, prototypes) | Product + UI/UX | Approved wireframes |
| **Week 5-6** | Development + testing | Mobile Dev Team | Launch ready |

**Phase 2 Impact:** Revenue +₹30-40 lakhs/month additional

---

## SUCCESS METRICS & KPIs

| **KPI** | **Current** | **Target (90 days)** | **Owner** | **Tracking** |
|---|---|---|---|---|
| Cart Abandonment Rate | 45% | 35% | Product Manager | Analytics Dashboard |
| Checkout Conversion | 23.1% | 35-40% | Product Manager | E-commerce Platform |
| Mobile Completion Rate | 15% | 30% | Product Manager | Segment by device |
| Support Tickets (Checkout) | 127/month | <50/month | Support Manager | Ticket System |
| App/Website Rating | — | 4.2+ | Marketing Manager | App Stores |

---

## BUDGET ESTIMATE

| **Item** | **Cost** | **Type** |
|---|---|---|
| Frontend Development (Phase 1) | ₹5,00,000 | One-time |
| WhatsApp Business API | ₹50,000 | One-time |
| WhatsApp Monthly | ₹10,000 | Monthly |
| A/B Testing Tool | ₹30,000 | One-time |
| Mobile Optimization (Phase 2) | ₹15,00,000 | One-time |
| QA & Testing | ₹3,00,000 | One-time |
| Contingency (10%) | ₹2,50,000 | One-time |
| **TOTAL** | **₹27,40,000** | **~₹10,000/month ongoing** |

### ROI Analysis

**Phase 1 Investment:** ₹8,00,000  
**Phase 1 Return (Month 1):** ₹34,00,000 (revenue recovery)  
**Phase 1 ROI:** 4,150% in first month

**Total Investment (Phase 1+2):** ₹27,40,000  
**3-Month Return:** ₹1,02,00,000+ (revenue recovery)  
**Total ROI:** 373% in 3 months  
**Payback Period:** <1 week

---

## APPROVAL & SIGN-OFF

| **Stakeholder** | **Role** | **Approval** | **Date** |
|---|---|---|---|
| CEO | Decision Maker | ☐ Approved | _____ |
| CTO | Technology Owner | ☐ Approved | _____ |
| Product Manager | Project Owner | ☐ Approved | _____ |
| Finance Lead | Budget Owner | ☐ Approved | _____ |

---

## APPENDIX: CURRENT vs IMPROVED CHECKOUT FLOW

### Current (5-Step, 8-10 mins average)
1. Add product to cart
2. Click "Proceed" (30% abandon here)
3. Enter shipping address (manually type)
4. Select shipping method (hidden cost appears!) → 32% abandon here
5. Enter billing address
6. Enter card details
7. Review order
8. Place order
9. Payment confirmation

### Improved (3-Step, 2-3 mins average)
1. **Shipping Info** (auto-filled, edit if needed) + display cost + delivery date
2. **Payment** (show all options, one-click available)
3. **Confirmation** (order placed successfully)

---

*Document Version: 1.0*  
*Last Updated: October 2025*
