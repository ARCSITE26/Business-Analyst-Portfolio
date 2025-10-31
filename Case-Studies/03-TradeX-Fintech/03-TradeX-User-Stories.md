# TradeX Securities — Platform Turnaround
## User Stories & Acceptance Criteria

---

## USER STORY #1: Fast Order Execution for Active Traders

**Priority:** CRITICAL | **Business Value:** ₹45 crores/year | **Complexity:** HIGH

```
As an active intraday trader,
I want my market orders to execute in <1 second,
So that I can enter/exit positions at desired prices without slippage during high volatility.
```

### Acceptance Criteria

**Execution Speed:**
- ✅ Order execution time <1 second during 9:30 AM - 3:30 PM (normal market hours)
- ✅ Order execution time <2 seconds during 9:15-9:30 AM (market open volatility)
- ✅ Order execution time <3 seconds during 3:30-4:00 PM (market close)
- ✅ P99 latency (worst case): <2.5 seconds

**Order Confirmation:**
- ✅ Real-time order status updates in app (no delay)
- ✅ User sees "Order Placed" confirmation within 500ms of submission
- ✅ Trade confirmation sent via push notification within 1 second

**Reliability:**
- ✅ Order rejection rate: <0.5% (currently 3%)
- ✅ Failed orders automatically retry (max 2 retries, 100ms intervals)
- ✅ Zero loss of orders (100% delivery guarantee)

**Load Handling:**
- ✅ System handles 10,000 concurrent orders/second
- ✅ No performance degradation during market open spike
- ✅ Database can handle 100,000 transactions/second

**Integration:**
- ✅ Works across all order types: Market, Limit, Stop-Loss, Bracket
- ✅ Works on both Android and iOS apps
- ✅ Works on web platform (no advantage to mobile only)

### Technical Implementation

**Current State:** 2-8 seconds average execution time (vs competitors <1 second)  
**Root Cause:** Legacy Order Management System (10-year-old monolith)  
**Solution:** Rebuild OMS with distributed architecture

**Components to Build:**
1. Order routing optimization (reduce processing steps)
2. Database distributed for concurrent processing
3. Caching layer (frequently used data cached in-memory)
4. Load balancers (distribute traffic across servers)

### Business Impact

**User Segment:** Active Traders (35% of users, ₹600/month ARPU, but 15% churn)  
**Revenue Impact:** Currently losing to Zerodha/Upstox. Fix this → retain 500K traders → ₹45 crores/year

**Success Metrics:**
- Execution complaints: 700/month → <100/month
- Churn rate for active traders: 18% → 10%
- App rating improvement: 3.8 → 4.1+ (from this feature alone)
- MAU increase: 35% → 40% (traders feel confident to trade more)

### Dependencies

- **CTO approval** (major architecture change)
- **Infrastructure upgrade** (new servers, databases)
- **SEBI compliance review** (order routing must follow regulations)
- **Payment for cloud infrastructure** (AWS/GCP premium tier)

### Effort Estimate

- **Phase 1 (Month 1-2):** Infrastructure setup + database migration: 400 hours
- **Phase 2 (Month 3-4):** OMS rebuild + API optimization: 600 hours
- **Phase 3 (Month 5-6):** Testing + performance tuning: 300 hours
- **Total:** 6-9 months, 2-3 developers full-time

---

## USER STORY #2: App Stability During Market Volatility

**Priority:** CRITICAL | **Business Value:** ₹35 crores/year | **Complexity:** MEDIUM

```
As a trader,
I want the app to NOT crash during market open and high volatility,
So that I can place orders when opportunities arise and don't lose money due to app failure.
```

### Acceptance Criteria

**Stability Metrics:**
- ✅ App uptime: 99.5%+ (currently 98.5%)
- ✅ Zero crashes during 9:15-9:30 AM market open
- ✅ Zero crashes during >10% market swings (circuit breakers)
- ✅ App responsive time: <500ms for UI interactions

**Load Testing:**
- ✅ System handles 50,000 concurrent app sessions
- ✅ Real-time data updates (quotes, P&L) with <100ms delay
- ✅ No memory leaks (app doesn't use increasing RAM over time)

**Error Handling:**
- ✅ If backend is down, app shows clear "Server temporarily unavailable" message
- ✅ No data corruption if app crashes mid-order
- ✅ Pending orders recovered when app restarts

**Performance:**
- ✅ App startup time: <3 seconds (currently 5+ seconds)
- ✅ Quote updates: 1-2 updates/second (no lag)
- ✅ Chart rendering: Smooth scrolling, no stuttering

### Technical Implementation

**Current Issues:**
- Server overload during market open (insufficient capacity)
- Memory leaks in real-time data streaming module
- UI thread blocking (too much calculation on main thread)

**Solutions:**
1. Infrastructure scaling (auto-scaling during peak hours)
2. Code optimization (move heavy processing to background threads)
3. Caching (store frequently accessed data locally)
4. Load testing (identify and fix bottlenecks)

### Business Impact

**User Segment:** All traders (affects casual + active + power traders)  
**Revenue Impact:** App crashes drive churn; 22% cite crashes as reason for switching  
**Revenue Save:** Prevent 500K churned traders → ₹35 crores/year

**Success Metrics:**
- Crash complaints: 550/month → <50/month
- App rating: 3.8 → 4.0+
- MAU increase: 35% → 42% (traders feel confident to use app)
- Churn reduction: 18% → 15%

### Effort Estimate

- **Analysis + Planning:** 1 month
- **Infrastructure scaling:** 1 month (hire DevOps/cloud engineers)
- **Code optimization:** 2 months (mobile development team)
- **Total:** 3-4 months, 2-3 developers

---

## USER STORY #3: Advanced Charting (TradingView Integration)

**Priority:** HIGH | **Business Value:** ₹15 crores/year | **Complexity:** MEDIUM

```
As an active trader,
I want TradingView-level charting with 100+ technical indicators,
So that I can perform technical analysis and identify trading opportunities like I can on Zerodha.
```

### Acceptance Criteria

**Charting Features:**
- ✅ Real-time candlestick charts (1-min, 5-min, 15-min, hourly, daily)
- ✅ 100+ technical indicators (Moving Average, RSI, MACD, Bollinger Bands, etc.)
- ✅ Drawing tools (trendlines, support/resistance levels, channels)
- ✅ Zoom + pan smoothly without lag
- ✅ Overlay multiple indicators simultaneously

**Data Quality:**
- ✅ Real-time price updates (every tick)
- ✅ Historical data available (5 years back minimum)
- ✅ No chart lag during high-volatility periods

**Integration:**
- ✅ Works on mobile (iOS/Android)
- ✅ Works on web platform
- ✅ Synchronized across devices (chart on web = same on mobile)

### Technical Implementation

**Current State:** Basic charting (10 indicators, 1-2 second lag)  
**Solution:** Integrate TradingView Lightweight Charts (white-label)

**Options:**
1. **TradingView Partnership:** $500-1000/month, fully managed
2. **Build custom:** 3-4 months development, ongoing maintenance
3. **Lightweight Charts SDK:** Free open-source, requires customization

### Business Impact

**User Segment:** Active Traders (35% of users, demand advanced charting)  
**Revenue Impact:** 12% of complaints cite "lack of advanced charting"  
**Revenue Save:** Prevent churn of power traders → ₹15 crores/year

**Success Metrics:**
- Charting complaints: 300/month → <50/month
- Active traders using charting feature: 40% → 70%
- ARPU increase for traders using charting: ₹650 → ₹850

### Effort & Cost

- **Integration:** 1 month (if using TradingView partnership)
- **Cost:** ₹5-10 lakhs/month (TradingView license)
- **Or:** 3-4 months development (if building custom)

---

## USER STORY #4: Algo Trading & API Access

**Priority:** HIGH | **Business Value:** ₹25 crores/year | **Complexity:** VERY HIGH

```
As a power trader / developer,
I want REST API access to place algorithmic orders programmatically,
So that I can build trading bots and automate my trading strategies (like Zerodha's Kite Connect).
```

### Acceptance Criteria

**API Endpoints:**
- ✅ `/place_order` - Place market, limit, and bracket orders
- ✅ `/cancel_order` - Cancel pending orders
- ✅ `/place_algo_order` - Place algorithmic/basket orders
- ✅ `/portfolio` - Get current holdings and P&L
- ✅ `/quotes` - Get real-time stock quotes
- ✅ `/orders` - Get order history and status

**Reliability:**
- ✅ API uptime: 99.9%
- ✅ Order latency: <500ms
- ✅ WebSocket for live data (low latency updates)
- ✅ Rate limiting: 100 requests/second per user (prevent abuse)

**Security:**
- ✅ OAuth 2.0 authentication
- ✅ Rate limiting per API key
- ✅ IP whitelisting option
- ✅ API key rotation capability

**Documentation:**
- ✅ Comprehensive API docs (OpenAPI/Swagger format)
- ✅ Code samples (Python, Node.js, Java)
- ✅ Webhook support (order updates pushed to user URL)

### Technical Implementation

**Complexity:** VERY HIGH (requires architecture redesign)

**Components:**
1. API Gateway (Kong, AWS API Gateway)
2. Authentication layer (OAuth 2.0)
3. Rate limiting + throttling
4. WebSocket server (for live updates)
5. Documentation + SDKs

### Business Impact

**User Segment:** Power Traders (15% of users, but 40% of revenue)  
**Revenue Impact:** Power traders churning to Zerodha for API access  
**Revenue Save:** Retain 50K power traders → ₹25 crores/year

**Success Metrics:**
- Power traders using API: 10K → 50K
- API transaction volume: 1M orders/month → 20M orders/month
- ARPU increase for API users: ₹1,500 → ₹2,000

### Effort Estimate

- **Design + Architecture:** 1 month
- **API development:** 2-3 months
- **Testing + documentation:** 1 month
- **Total:** 4-5 months, 3-4 developers

### Dependencies

- **SEBI approval** (6-month regulatory process, start in M1)
- **CTO sign-off** (architectural change)
- **Security audit** (API security review required)

---

## USER STORY #5: Instant Fund Transfer (UPI Integration)

**Priority:** HIGH | **Business Value:** ₹8 crores/year | **Complexity:** LOW

```
As a trader,
I want to deposit funds via UPI instantly (not 24-hour NEFT),
So that I can quickly start trading when I see opportunities.
```

### Acceptance Criteria

**UPI Transfer:**
- ✅ UPI deposit option available in app
- ✅ Funds credit: Instant (0-5 minutes max)
- ✅ Works 24/7/365 (including weekends, holidays)
- ✅ UPI limit: ₹2 lakhs per transaction (NPCI standard)
- ✅ Error handling: Clear messages if transfer fails

**Payout (Withdrawal):**
- ✅ Withdraw to any UPI ID
- ✅ Instant transfer (0-2 minutes)
- ✅ Low/no fees (competitive vs competitors)

### Technical Implementation

**Current State:** 24-hour NEFT only  
**Solution:** Integrate Razorpay or PayU UPI gateway

**Vendors:**
- Razorpay: 2% + ₹5 commission
- PayU: 3% + ₹2 commission
- BharatQR: 1.1% + ₹5 commission

### Business Impact

**Revenue Impact:** Low friction = more deposits = more trading activity  
**Revenue Save:** Only 2% of complaints but table-stakes feature  
**Estimated gain:** ₹8 crores/year (from increased trading volume)

### Effort & Cost

- **Integration:** 1-2 weeks (straightforward API integration)
- **Cost:** ₹50-100 lakhs/year (transaction fees to UPI provider)
- **ROI:** 8-16x in Year 1

---

*Document Version: 1.0 | Last Updated: October 2025*
