# QUANTUM Trading Intelligence System — Master Project Blueprint

**Document:** Master Blueprint  
**Blueprint Version:** 1.1 (Post-Audit Technical Revision)  
**Project Owner:** Founder  
**Approval Authority:** Founder  
**Development Method:** Step-by-Step, Phase-by-Phase  
**Current Project Status:** `DESIGNED` (Blueprint Only — `NOT IMPLEMENTED`)  

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Project Vision](#2-project-vision)
3. [Objectives](#3-objectives)
4. [Locked Configuration](#4-locked-configuration)
5. [Supported Markets](#5-supported-markets)
6. [Nine Timeframes Architecture](#6-nine-timeframes-architecture)
7. [Execution Timeframe Selection](#7-execution-timeframe-selection)
8. [Independent Timeframe Signals (Mode A)](#8-independent-timeframe-signals-mode-a)
9. [Multi-Timeframe Confirmation (Mode B)](#9-multi-timeframe-confirmation-mode-b)
10. [Trading Methodology](#10-trading-methodology)
11. [Twelve Brains Intelligence Core](#11-twelve-brains-intelligence-core)
12. [Institutional & Smart Money Concepts (SMC) Architecture](#12-institutional--smart-money-concepts-smc-architecture)
13. [Multi-Timeframe (MTF) Intelligence Architecture](#13-multi-timeframe-mtf-intelligence-architecture)
14. [Master Decision Engine](#14-master-decision-engine)
15. [Entry, Execution, and Risk Management](#15-entry-execution-and-risk-management)
16. [News Intelligence](#16-news-intelligence)
17. [Market Protection System](#17-market-protection-system)
18. [Website Architecture & UI/UX Design System](#18-website-architecture--uiux-design-system)
19. [TradingView & Pine Script v6 Integration](#19-tradingview--pine-script-v6-integration)
20. [Frontend Architecture](#20-frontend-architecture)
21. [Backend Architecture](#21-backend-architecture)
22. [Database Architecture & Entity-Relationship Design](#22-database-architecture--entity-relationship-design)
23. [API Architecture](#23-api-architecture)
24. [Security Architecture & Threat Model](#24-security-architecture--threat-model)
25. [Market Data Architecture & Provider Evaluation](#25-market-data-architecture--provider-evaluation)
26. [User Roles & Extensible Permission System](#26-user-roles--extensible-permission-system)
27. [Phase 0–9 Complete Development Roadmap](#27-phase-09-complete-development-roadmap)
28. [Phase Dependencies & Execution Graph](#28-phase-dependencies--execution-graph)
29. [Testing Architecture](#29-testing-architecture)
30. [Backtesting, Walk-Forward, and Optimization Framework](#30-backtesting-walk-forward-and-optimization-framework)
31. [Deployment, Hosting, and Infrastructure](#31-deployment-hosting-and-infrastructure)
32. [Logging, Monitoring, and Observability](#32-logging-monitoring-and-observability)
33. [Backup, Disaster Recovery, and Business Continuity](#33-backup-disaster-recovery-and-business-continuity)
34. [Founder Approval System & Governance](#34-founder-approval-system--governance)
35. [Known Limitations & Technical Risks](#35-known-limitations--technical-risks)
36. [Pending Founder Decisions](#36-pending-founder-decisions)
37. [Future Expansion & Modular Broker Adapters](#37-future-expansion--modular-broker-adapters)
38. [Current Project Status &Intended Repository Structure](#38-current-project-status--intended-repository-structure)
39. [Development Workflow & Change Control](#39-development-workflow--change-control)

---

## 1. Project Overview

**QUANTUM Trading Intelligence** is an institutional-grade, multi-market analytical and decision-support platform designed to evaluate financial markets—specifically **XAUUSD (Spot Gold vs. US Dollar)** and **BTCUSD (Bitcoin vs. US Dollar)**—across nine distinct timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`).

Rather than relying on single-indicator triggers or black-box predictions, QUANTUM employs a deterministic, auditable **12-Brain Intelligence Core** combined with **Smart Money Concepts (SMC)**, **Multi-Timeframe (MTF) Alignment**, **Macroeconomic & Crypto News Protection**, and a **Strict Risk Management Engine**. The system evaluates market state on confirmed candle closes to emit explainable, non-repainting decisions: **`BUY`**, **`SELL`**, or **`WAIT`**.

### Core System Pillars
- **Explainable Intelligence:** Every decision (`BUY`, `SELL`, or `WAIT`) includes a structured audit trail detailing the exact vote of all 12 analytical brains, confidence metrics, SMC confirmations, MTF alignment state, and invalidation levels.
- **Confirmed-Only Execution:** All calculations run strictly on closed, validated candles (`barstate.isconfirmed` in Pine Script v6 and verified close timestamps in the backend) to eliminate repainting and lookahead bias.
- **Strict Separation of Voting and Confidence:** Each of the 12 brains casts an equal directional vote (`BUY`, `SELL`, or `NEUTRAL`) alongside a separate quantitative confidence score (`0.00` to `100.00`). Missing or corrupted data yields `DATA UNAVAILABLE` and abstains from voting rather than fabricating a synthetic vote.
- **Dual-Platform Parity:** Synchronized rulesets operating across a full-stack web platform (dashboards, historical backtester, strategy lab, risk calculators) and TradingView **Pine Script v6** indicators/alerts connected via authenticated webhooks.

---

## 2. Project Vision

Financial retail and semi-institutional trading tools frequently fail due to three structural flaws: signal repainting, lack of multi-timeframe context, and absence of automated risk/news protection. QUANTUM's vision is to engineer a transparent, institutional-style trading intelligence architecture that prioritizes capital preservation and analytical rigor above signal frequency.

### Guiding Principles
1. **Reliable Analysis Over Hype:** QUANTUM makes **no promises of guaranteed profits, guaranteed accuracy, or fixed win rates**. Financial markets are probabilistic; QUANTUM is engineered to enforce disciplined execution, quantifiable risk-to-reward profiles, and objective structural validation.
2. **Confirmed Signals Only:** Zero tolerance for intrabar flickering signals or retroactive chart repainting.
3. **Risk Control First:** Every `BUY` or `SELL` output is paired with mathematically defined Entry Zones, Stop Loss (`SL`), Take Profit levels (`TP1`, `TP2`, `TP3`), Position Sizing, Invalidation criteria, and automated vetoes during high-impact news or abnormal spread/volatility regimes.
4. **Data Validation & Integrity:** Strict verification of incoming OHLCV candles, timestamps, gaps, and provider latency. When feeds fail or disconnect, the system explicitly reports `DATA UNAVAILABLE` or `NOT CONNECTED` and defaults to `WAIT`.
5. **Founder-Controlled Governance:** Every architectural milestone, parameter baseline, UI theme selection, and phase transition is gated by explicit Founder review and approval.

---

## 3. Objectives

| Objective Category | Specific Engineering & Product Target | Verification Metric / Acceptance Criteria |
| :--- | :--- | :--- |
| **Analytical Precision** | Implement 12 independent analytical brains with zero overlapping double-counting of evidence. | 100% unit test coverage per brain; deterministic output for identical historical OHLCV inputs. |
| **Multi-Market Isolation** | Independent parameter profiles, pip/tick math, session definitions, and news filters for `XAUUSD` and `BTCUSD`. | Separate configuration schemas and database records per symbol; zero cross-contamination. |
| **Nine-Timeframe Native Support** | Full ingestion, analysis, storage, and UI selection across `1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`. | Distinct database composite keys `(symbol, timeframe, timestamp)` and isolated timeframe execution pipelines. |
| **Zero Repainting / Zero Lookahead** | Prevent future candle leakage in MTF alignments and historical backtests. | Automated lookahead-bias test suite comparing bar-by-bar sequential replay against batch historical runs. |
| **Explainability** | Every `BUY`, `SELL`, and `WAIT` decision logs full JSON breakdown and human-readable reasoning. | Every signal record contains all 12 brain outputs, MTF matrix, SMC tags, risk plan, and veto reasons. |
| **Capital & News Protection** | Automatically block or invalidate trade setups during Tier-1 macro events, spread spikes, or daily drawdown breaches. | Simulated high-impact news and drawdown unit tests verify forced `WAIT` state. |
| **Modular Extensibility** | Decouple core intelligence from data ingestion and future broker execution adapters. | Clean interface contracts allowing future broker adapters without altering Phase 1–5 engine code. |

---

## 4. Locked Configuration

The following configuration parameters are **locked** by the Founder. They cannot be silently modified by any future development phase. Any ambiguity or unapproved sub-parameter is marked `PENDING FOUNDER DECISION`.

| Setting | Locked Requirement | Governance / Notes |
| :--- | :--- | :--- |
| **Project** | QUANTUM Trading Intelligence | Master system identifier |
| **Primary Market 1** | `XAUUSD` | Spot Gold / US Dollar |
| **Primary Market 2** | `BTCUSD` | Bitcoin / US Dollar |
| **Trading Style** | Hybrid Sniper + Fast Scalper | Supports precision zone limit/confirmation entries and momentum displacement scalps |
| **Signal Mode** | Confirmed Only | Evaluations execute strictly on confirmed candle close |
| **Decision Mode** | `STRICT` | Requires mandatory minimum brain voting threshold + MTF/SMC/Risk non-veto |
| **Brain Voting** | Equal Voting | All 12 brains carry an equal weight of `1` vote initially (`1/12` each) |
| **Signal Directions** | `BUY`, `SELL`, `WAIT` | Every evaluation cycle must resolve to one of these three deterministic states |
| **Website** | Required | Full web platform with role-based dashboards |
| **Backend** | Required | Core intelligence engine, data ingestion, risk & decision service |
| **Database** | Required | Persistent relational + time-series storage |
| **TradingView** | Pine Script v6 | Custom indicator/strategy script + alert webhook integration |
| **Initial Access** | Private | Invite-only / Founder & Private Tester access initially |
| **Future Access** | Public after Founder approval | Gated by feature flags and explicit Phase 9 sign-off |
| **Initial Auto Trading** | Disabled | Decision-support, paper validation, and alert generation only at launch |
| **Future Broker Integration** | Modular architecture required | Abstract adapter interfaces designed in Phase 0/5 for future live execution |
| **Development Approval** | Founder controlled | Strict step-by-step phase gate approval required |
| **Default Execution Timeframe** | `PENDING FOUNDER DECISION` | System supports all 9 timeframes; default landing timeframe awaits Founder selection |
| **Minimum Brain Vote Threshold** | `PENDING FOUNDER DECISION` | Proposed baseline documented in Section 14; final threshold requires Founder sign-off |
| **UI Color Theme Concept** | `PENDING FOUNDER DECISION` | Concept A, B, or C documented in Section 18 awaits Founder selection |

---

## 5. Supported Markets

QUANTUM natively supports two primary instruments with radically different microstructure, liquidity schedules, volatility profiles, and macroeconomic drivers. Therefore, `XAUUSD` and `BTCUSD` must never share static thresholds.

### 5.1 Market Comparison & Microstructure Specification

| Attribute | Primary Market 1: `XAUUSD` (Gold) | Primary Market 2: `BTCUSD` (Bitcoin) |
| :--- | :--- | :--- |
| **Asset Class** | Spot Commodity / Precious Metal CFD / Bullion | Spot Cryptocurrency |
| **Authoritative Session & Settlement Timezone** | **`America/New_York`** (IANA timezone database; automatically handles US Daylight Saving Time `EDT = UTC-4` and US Standard Time `EST = UTC-5`). Internal storage remains `UTC`. | **`UTC`** (`Etc/UTC`, continuous 24/7/365 with zero DST offset). |
| **Trading Schedule & Daily Rollover Break** | 23 hours/day, 5 days/week: Opens Sunday `18:00 America/New_York` (`22:00 UTC` in EDT / `23:00 UTC` in EST) and closes Friday `17:00 America/New_York` (`21:00 UTC` in EDT / `22:00 UTC` in EST). Daily 1-hour CME/Bullion settlement & maintenance break occurs strictly from **`17:00 to 18:00 America/New_York`** (`21:00–22:00 UTC` during EDT; `22:00–23:00 UTC` during EST). | 24 hours/day, 7 days/week, 365 days/year (Continuous trading; no daily rollover break and no weekend close). |
| **Price Quotation & Tick Size** | Quoted in USD per Troy Ounce (typically 2 decimal places, e.g., `2650.45`, tick size `0.01`; broker-dependent `0.001`). | Quoted in fiat **USD** per 1 BTC (2 decimal places, e.g., `89450.00`, tick size `0.01` or `0.10` depending on feed). See Section 5.3 for strict `BTCUSD` vs. `BTCUSDT` separation. |
| **Primary Liquidity Sessions** | **Timezone-Aware Institutional Sessions:**<br>• **Asian Session:** `18:00–03:00 America/New_York` (`22:00–07:00 UTC` EDT / `23:00–08:00 UTC` EST)<br>• **London Session:** `08:00–16:30 Europe/London` (`07:00–15:30 UTC` BST / `08:00–16:30 UTC` GMT)<br>• **New York Session:** `08:00–17:00 America/New_York` (`12:00–21:00 UTC` EDT / `13:00–22:00 UTC` EST)<br>• **London/NY Overlap (Peak Volatility):** `08:00–12:00 America/New_York` (`12:00–16:00 UTC` when both US and UK are on summer time; dynamically computed via IANA intersection of London & NY active windows). | Global 24/7, with institutional volume clustering around US Equities Open (`09:30–16:00 America/New_York`), European Hours (`08:00–16:30 Europe/London`), Asian Hours (`00:00–08:00 UTC`), and CME BTC Futures settlement windows. |
| **Daily Candle (`1D`) Close Reference** | **`17:00:00 America/New_York`** (New York Institutional Close: `21:00:00 UTC` in EDT; `22:00:00 UTC` in EST) to align with global bullion settlement and prevent artificial 2-hour Sunday candles. | **`00:00:00 UTC`** standard institutional crypto daily close. |
| **4-Hour (`4H`) Candle Alignment Convention** | **Authoritative System Default: Strict 4-Hour UTC Modulo Grid** (`00:00, 04:00, 08:00, 12:00, 16:00, 20:00 UTC`) across both backend and TradingView charts for deterministic cross-provider reproducibility. Optional NY-session-anchored `4H` aggregation (`18:00, 22:00, 02:00, 06:00, 10:00, 14:00 America/New_York`) is documented in Section 6.4. | **Strict 4-Hour UTC Modulo Grid** (`00:00, 04:00, 08:00, 12:00, 16:00, 20:00 UTC`). |
| **Typical Volatility Driver** | US Dollar Index (DXY), US Treasury Real Yields (US10Y), Fed Rates, CPI/NFP, Geopolitical risk. | Spot ETF inflows/outflows, Exchange perp funding rates, Open Interest liquidations, Regulatory news, Macro liquidity. |
| **Weekend Gap Behavior** | Prone to Friday `17:00 America/New_York` to Sunday `18:00 America/New_York` opening price gaps requiring weekend gap-aware candle validation. | Trades continuously through weekends; CME futures weekend gap proxies tracked separately as informational liquidity magnets if enabled. |
| **Contract / Lot Specification** | Standard Lot = 100 Troy Ounces (`0.01` move = `$1.00` per standard lot; broker verification required). | 1 Standard Unit = 1.00 BTC (`1.00` USD move = `$1.00` per 1 BTC; exchange/broker verification required). |

### 5.2 Authoritative `XAUUSD` DST & Timezone Resolution Rule
A common flaw in trading systems is hardcoding New York `17:00` close as a static `21:00 UTC` year-round. In reality:
- During **US Daylight Saving Time (`EDT`, 2nd Sunday in March to 1st Sunday in November):** `17:00 America/New_York = 21:00 UTC` (Daily rollover break: `21:00–22:00 UTC`).
- During **US Standard Time (`EST`, 1st Sunday in November to 2nd Sunday in March):** `17:00 America/New_York = 22:00 UTC` (Daily rollover break: `22:00–23:00 UTC`).
- During the **US/UK DST Transition Mismatch Weeks** (2–3 weeks in March and 1 week in October/November where US and UK shift on different Sundays), QUANTUM never uses static UTC hour offsets for session killzones; all session boundaries (`London Open`, `NY Open`, `London/NY Overlap`, `NY Close Rollover`) are dynamically resolved at runtime from the candle's `UTC` timestamp using the `zoneinfo` (`America/New_York` and `Europe/London`) IANA timezone database.

### 5.3 Strict `BTCUSD` vs. `BTCUSDT` Quote-Currency Normalization Rules
`BTCUSD` (fiat US Dollar quote, e.g., Coinbase, Kraken, Bitstamp, CME, Twelve Data, Polygon) and `BTCUSDT` (Tether stablecoin quote, e.g., Binance Perp/Spot, Bybit) are **distinct financial instruments** that can diverge by several dollars to hundreds of dollars during stablecoin de-pegs or basis expansions:
1. **No Implicit Equivalence:** QUANTUM never treats a `BTCUSDT` price candle as identical to a `BTCUSD` price candle for Entry, Stop Loss, Take Profit, or Order Block price coordinates.
2. **Primary Price Canonicalization (`BTCUSD`):** All price levels (`Open`, `High`, `Low`, `Close`, `Entry`, `SL`, `TP1..3`, `OB`/`FVG` bounds, `BSL`/`SSL` pools) for the primary market `BTCUSD` must originate strictly from a verified **USD-quoted** `BTCUSD` feed.
3. **Auxiliary Derivatives & Volume Telemetry (`BTCUSDT` / Exchange Perps):** When a `BTCUSDT` spot or perpetual futures stream (such as Binance `BTCUSDT`) is connected to supply supplementary centralized exchange volume (`Brain 10 RVOL`) or derivatives funding/liquidation metrics (`Phase 6`), the adapter stores those metrics in a distinct `provider_symbol = 'BTCUSDT'` telemetry channel:
   - Dimensionless ratios (`RVOL`, `Funding Rate %`, `Normalized Liquidation Z-Score`) may be consumed as dimensionless inputs after timestamp alignment.
   - Raw `BTCUSDT` price levels are **never** merged into `BTCUSD` OHLC candles unless an explicit, live-verified `USDT/USD` spot conversion rate (`BTCUSD_implied = BTCUSDT * USDTUSD_mid`) is enabled and tagged as `SYNTHETIC_CONVERTED_FEED` (disabled by default in `STRICT` mode).

---

## 6. Nine Timeframes Architecture

QUANTUM enforces first-class architectural support for all **nine execution and analysis timeframes**.

### 6.1 Mandatory Timeframe Registry & Multi-Platform Mapping Matrix

To prevent fatal identifier collisions between internal QUANTUM storage (`1M` = 1 Minute, `1MO` = 1 Month) and TradingView Pine Script v6 (`"1"` = 1 Minute, `"1M"` = 1 Month), every internal service, database migration, Pine Script adapter, and external data provider adapter must enforce the following canonical translation table:

| Internal QUANTUM ID | Full Name | Duration / Calendar Rule | Candle Boundary Alignment | Pine Script v6 `timeframe.period` / `request.security()` String | Twelve Data `interval` | Polygon.io `multiplier` / `timespan` | OANDA v20 `granularity` | Binance / Crypto Klines `interval` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`1M`** | 1 Minute | `60 seconds` | Every minute at `:00` seconds UTC | **`"1"`** | `"1min"` | `1` / `"minute"` | `"M1"` | `"1m"` |
| **`5M`** | 5 Minutes | `300 seconds` | Minutes `:00, :05, :10, ..., :55` UTC | **`"5"`** | `"5min"` | `5` / `"minute"` | `"M5"` | `"5m"` |
| **`15M`** | 15 Minutes | `900 seconds` | Minutes `:00, :15, :30, :45` UTC | **`"15"`** | `"15min"` | `15` / `"minute"` | `"M15"` | `"15m"` |
| **`30M`** | 30 Minutes | `1,800 seconds` | Minutes `:00, :30` UTC | **`"30"`** | `"30min"` | `30` / `"minute"` | `"M30"` | `"30m"` |
| **`1H`** | 1 Hour | `3,600 seconds` | Top of every hour `HH:00:00` UTC | **`"60"`** | `"1h"` | `1` / `"hour"` | `"H1"` | `"1h"` |
| **`4H`** | 4 Hours | `14,400 seconds` | Authoritative Default: `00:00, 04:00, 08:00, 12:00, 16:00, 20:00 UTC` (See Section 6.4) | **`"240"`** | `"4h"` | `4` / `"hour"` | `"H4"` | `"4h"` |
| **`1D`** | 1 Day | `1 Trading Day` (DST-aware for XAUUSD; `86,400s` for BTCUSD) | `00:00:00 UTC` (`BTCUSD`) / `17:00:00 America/New_York` (`XAUUSD`) | **`"1D"`** (or `"D"`) | `"1day"` | `1` / `"day"` | `"D"` | `"1d"` |
| **`1W`** | 1 Week | `1 Calendar / Trading Week` | Monday `00:00:00 UTC` (`BTCUSD`) / Sunday `18:00:00 America/New_York` to Friday `17:00:00 America/New_York` (`XAUUSD`) | **`"1W"`** (or `"W"`) | `"1week"` | `1` / `"week"` | `"W"` | `"1w"` |
| **`1MO`** | 1 Month | `1 Calendar Month` (`28, 29, 30, or 31 days`) | 1st calendar day `00:00:00 UTC` (or first trading session after end-of-month `17:00 America/New_York` for `XAUUSD`) | **`"1M"`** (or `"M"`) | `"1month"` | `1` / `"month"` | `"M"` | `"1M"` |

### 6.2 Strict Identifier Disambiguation & Translation Boundary Rule
1. **Internal QUANTUM Standard:**
   - **`1M` strictly and exclusively denotes 1 Minute.**
   - **`1MO` strictly and exclusively denotes 1 Month.**
2. **Pine Script v6 & External Provider Boundary Translation:**
   - In TradingView Pine Script v6, `timeframe.period == "1"` represents 1 Minute, while `timeframe.period == "1M"` represents 1 Month.
   - The Pine Script v6 script and the Backend Webhook Receiver (`POST /api/v1/webhooks/tradingview`) include an explicit bidirectional translator function `map_pine_tf_to_quantum_tf(pine_tf)`:
     - Pine `"1"` $\leftrightarrow$ QUANTUM `"1M"`
     - Pine `"5"` $\leftrightarrow$ QUANTUM `"5M"`
     - Pine `"15"` $\leftrightarrow$ QUANTUM `"15M"`
     - Pine `"30"` $\leftrightarrow$ QUANTUM `"30M"`
     - Pine `"60"` $\leftrightarrow$ QUANTUM `"1H"`
     - Pine `"240"` $\leftrightarrow$ QUANTUM `"4H"`
     - Pine `"D"` or `"1D"` $\leftrightarrow$ QUANTUM `"1D"`
     - Pine `"W"` or `"1W"` $\leftrightarrow$ QUANTUM `"1W"`
     - Pine `"M"` or `"1M"` $\leftrightarrow$ QUANTUM `"1MO"`
   - The Pine Script webhook payload must always serialize the canonical internal QUANTUM identifier (`"1M"` for 1 Minute, `"1MO"` for 1 Month) in the `execution_timeframe` JSON field alongside `raw_pine_timeframe` so the backend can cross-verify both fields and reject any mismatch.

### 6.3 Timeframe-Specific Configuration Isolation
A parameter configuration suitable for `1M` (where noise is high and ATR is small) is invalid for `1D` or `1MO`. Therefore, every timeframe maintains an isolated configuration profile in the database per market symbol (`9 timeframes × 2 markets = 18 distinct baseline configuration profiles`):
1. **Indicator Parameters:** Lookback periods for ATR, EMA, RSI/Momentum, Volume moving averages.
2. **Structure Sensitivity:** Minimum swing pivot depth (`leftBars`, `rightBars`) and minimum ATR displacement required to validate a Break of Structure (`BOS`).
3. **Liquidity Sensitivity:** Tolerance in ATR multiples or ticks for Equal Highs (`EQH`) and Equal Lows (`EQL`), plus minimum sweep wick penetration and rejection ratio.
4. **Volatility Thresholds:** Minimum ATR percentile floor (dead market filter) and maximum ATR percentile ceiling (shock expansion veto).
5. **Confirmation Rules:** Required candle body-to-range ratio and displacement velocity.
6. **Entry, Stop Loss, and Take Profit Rules:** Buffer distances in ATR/ticks, maximum acceptable entry zone width, and R-multiple targets (`TP1`, `TP2`, `TP3`).
7. **Signal Expiry:** Maximum number of bars a pending Entry Zone remains valid before automatic expiration (`e.g., 6 bars on 1M vs. 3 bars on 1D`).
8. **Risk Parameters:** Maximum allowed spread-to-SL ratio (e.g., spread cannot exceed X% of SL distance on `1M`).

### 6.4 Authoritative `4H` Candle Boundary Convention (`XAUUSD` & `BTCUSD`)
Because different charting platforms align `4H` candles either to the `00:00 UTC` modulo-4 grid or to the `17:00/18:00 America/New_York` session open, QUANTUM establishes a single authoritative system rule:
1. **Authoritative System Standard (`UTC_MODULO_4H`):** By default, all `4H` candles for both `XAUUSD` and `BTCUSD` open and close strictly on the **4-hour UTC clock grid**: `00:00, 04:00, 08:00, 12:00, 16:00, 20:00 UTC`. During the daily 1-hour `XAUUSD` maintenance break (`17:00–18:00 America/New_York`), the `20:00–00:00 UTC` 4H bar simply contains the 3 active trading hours within that 4-hour UTC window. This matches standard UTC-based data providers (Twelve Data, Polygon) and UTC-configured charts.
2. **Optional Broker/NY-Aligned Mode (`NY_SESSION_4H`):** If a connected broker feed (such as OANDA v20 `H4` aligned to `17:00 America/New_York`) is selected by the Founder, the `ingestion_service` aggregates `4H` bars from verified `1H` bars anchored to `17:00 America/New_York` (`17:00, 21:00, 01:00, 05:00, 09:00, 13:00 America/New_York`) and tags the candle stream with `alignment_mode = 'NY_SESSION_4H'`. The backend and Pine Script v6 indicator must always share the same active `alignment_mode` setting from `system_settings` so `4H` Order Blocks and Swing Pivots match 100%.

---

## 7. Execution Timeframe Selection

### 7.1 Functional Specification
- **Purpose:** Allow authorized users (and automated evaluation workers) to select any of the nine timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`) as the active **Execution Timeframe**.
- **Function:** Switching the Execution Timeframe dynamically re-scopes the live chart, the 12-Brain analysis matrix, SMC zone overlays, MTF confirmation hierarchy, entry/SL/TP calculations, signal history feed, and performance analytics strictly to the selected timeframe.
- **Default Execution Timeframe:** `PENDING FOUNDER DECISION`.
- **Inputs:** `symbol` (`XAUUSD` | `BTCUSD`), `execution_timeframe` (`1M` | `5M` | `15M` | `30M` | `1H` | `4H` | `1D` | `1W` | `1MO`), `signal_mode` (`MODE_A_INDEPENDENT` | `MODE_B_MTF_CONFIRMED`).
- **Processing:**
  1. Validates that the user has permission to view/select the requested market and timeframe.
  2. Queries the latest confirmed analysis state and candle stream for `(symbol, execution_timeframe)`.
  3. If `MODE_B_MTF_CONFIRMED` is active, loads the configured higher/lower confirmation timeframes mapped to that `execution_timeframe`.
  4. Renders timeframe-stamped signal cards and trade plans.
- **Outputs:** Scoped state payload explicitly tagged with `execution_timeframe`, `candle_close_timestamp`, and `signal_mode`.
- **Validation:** Rejects any API response or UI render where `payload.execution_timeframe !== selected_execution_timeframe`.
- **Error Handling:** If the selected timeframe lacks the minimum required historical warm-up bars (minimum 200 confirmed candles for standard operation; see Section 11.2 Brain 1 for 200–249 vs. 250+ bar tiers and Section 25.4 for `1MO` deep-history requirements), the system displays `DATA UNAVAILABLE — INSUFFICIENT HISTORICAL BARS FOR [TIMEFRAME]` and forces decision state to `WAIT`.
- **Testing & Acceptance Criteria:** Switching from `5M` to `4H` must immediately display `4H`-specific structure, `4H` brain votes, `4H` entry/SL/TP distances, and `4H` historical metrics with zero cross-timeframe contamination.

---

## 8. Independent Timeframe Signals (Mode A)

### 8.1 Mode A Specification & Brain 2 Behavior in Mode A
- **Purpose:** Evaluate a single selected Execution Timeframe (`T_exec`) completely on its own merits without external higher-timeframe or lower-timeframe dependencies.
- **Function:** Produces an independent `BUY`, `SELL`, or `WAIT` signal strictly from the OHLCV, structure, liquidity, SMC, momentum, volatility, and news protection state of the selected timeframe `T_exec`.
- **Signal Type Label:** Every Mode A output is explicitly badged and stored in the database as `SIGNAL_TYPE: INDEPENDENT_TIMEFRAME`.
- **Authoritative Rule for Brain 2 (`BRAIN_02_MTF`) in Mode A:**
  - Because Mode A is strictly defined as an **Independent Timeframe Evaluation**, injecting Higher Timeframe (`HTF`) votes into a Mode A decision would violate Mode A isolation.
  - Therefore, when `signal_mode == 'INDEPENDENT_TIMEFRAME'` (Mode A):
    1. **Brain 2 (`BRAIN_02_MTF`) is formally designated `INACTIVE_IN_MODE_A` and casts `vote = 'NEUTRAL'`, `confidence = 0.00`** (with explanation `"Mode A Independent Timeframe active: HTF voting bypassed to preserve single-timeframe isolation; informational HTF telemetry logged separately"`).
    2. **Active Voting Pool in Mode A:** The 11 single-timeframe brains (`Brain 1` and `Brains 3 through 12`) cast directional votes (`BUY`, `SELL`, `NEUTRAL`, or `ABSTAIN_DATA_UNAVAILABLE`), each with an equal voting weight of `1` (`11` maximum active directional votes, plus Brain 2 fixed at `NEUTRAL`).
    3. **Equal Voting Consistency:** As detailed in Section 14.2, the Master Decision Engine scales the required consensus ratio consistently across active eligible brains (e.g., baseline `8/12` in Mode B corresponds to `8/11` in Mode A, or the exact integer threshold approved by the Founder per mode) so Mode A remains equally strict without ever leaking HTF bias into an independent timeframe signal.
- **Isolation Guarantee:**
  - `1M` Independent Analysis evaluates only `1M` candles and `1M` parameters.
  - `1H` Independent Analysis evaluates only `1H` candles and `1H` parameters.
  - `1MO` Independent Analysis evaluates only `1MO` candles and `1MO` parameters.
- **Separate Persistence & Statistics:** Mode A signals, trade plans, win rates, drawdowns, and backtest runs are stored and queried separately from Mode B signals so performance statistics are never conflated.

---

## 9. Multi-Timeframe Confirmation (Mode B)

### 9.1 Mode B Specification
- **Purpose:** Filter and confirm potential execution setups on the selected Execution Timeframe (`T_exec`) against the structural bias, liquidity draw, and order flow of mapped Higher Timeframes (`HTF`) and/or precision trigger alignment on Lower Timeframes (`LTF`).
- **Function:** When `T_exec` generates a candidate `BUY` or `SELL` setup, the MTF Confirmation Engine evaluates the mapped confirmation timeframes (`HTF 1`, `HTF 2`, and optional `LTF`). If a conflicting condition is detected (e.g., `T_exec` signals `BUY` directly into an unmitigated `HTF 1` Bearish Order Block or against `HTF 1` confirmed bearish BOS), Mode B vetoes the trade and outputs `WAIT` with an explicit conflict explanation.
- **Signal Type Label:** Every Mode B output is explicitly badged and stored as `SIGNAL_TYPE: MTF_CONFIRMED`.

### 9.2 Configurable Nine-Timeframe Relationship Matrix (Zero Self-Reference / Zero Duplication)
Every timeframe mapping in QUANTUM obeys three strict invariants:
1. **No Self-Reference:** An Execution Timeframe (`T_exec`) must **never** list itself as `HTF 1`, `HTF 2`, or `LTF` (`T_exec != HTF_1`, `T_exec != HTF_2`, `T_exec != LTF`).
2. **No HTF Duplication:** `HTF 1` and `HTF 2` must **never** reference the same timeframe (`HTF_1 != HTF_2`). If only one higher timeframe exists above `T_exec` (as on `1W`), `HTF 2` is explicitly `NULL` (`NONE_TOP_OF_HIERARCHY`).
3. **Strict Ordering:** Whenever defined, `Duration(LTF) < Duration(T_exec) < Duration(HTF_1) < Duration(HTF_2)`. A lower timeframe (`LTF`) is **never** substituted as a higher timeframe (`HTF`).

| Selected Execution Timeframe (`T_exec`) | Primary Higher Timeframe (`HTF 1` — Tactical Structure) | Secondary Higher Timeframe (`HTF 2` — Macro Bias / Dealing Range) | Lower Timeframe (`LTF` — Optional Micro Refinement Inside `T_exec` POI) | Active HTF Count & Boundary Rule |
| :--- | :--- | :--- | :--- | :--- |
| **`1M`** | `5M` | `15M` | `NULL` (`NONE_BOTTOM_OF_HIERARCHY`) | **2 HTFs (`5M`, `15M`)**; no timeframe exists below `1M`. |
| **`5M`** | `15M` | `1H` | `1M` | **2 HTFs (`15M`, `1H`)** + `1M` LTF. |
| **`15M`** | `1H` | `4H` | `5M` | **2 HTFs (`1H`, `4H`)** + `5M` LTF. |
| **`30M`** | `1H` | `4H` | `15M` | **2 HTFs (`1H`, `4H`)** + `15M` LTF. |
| **`1H`** | `4H` | `1D` | `15M` | **2 HTFs (`4H`, `1D`)** + `15M` LTF. |
| **`4H`** | `1D` | `1W` | `1H` | **2 HTFs (`1D`, `1W`)** + `1H` LTF. |
| **`1D`** | `1W` | `1MO` | `4H` | **2 HTFs (`1W`, `1MO`)** + `4H` LTF. |
| **`1W`** | `1MO` | `NULL` (`NONE_TOP_OF_HIERARCHY`) | `1D` | **1 HTF (`1MO` only)**. Because `1MO` is the highest supported timeframe, `HTF 2` is `NULL` (never duplicated). Brain 2 and Phase 3 MTF evaluate `1W` strictly against `1MO` (`100%` of HTF weight assigned to `1MO`). |
| **`1MO`** | `NULL` (`NONE_TOP_OF_HIERARCHY`) | `NULL` (`NONE_TOP_OF_HIERARCHY`) | `1W` (LTF trigger refinement only — never treated as an HTF) | **0 HTFs (`TOP_OF_HIERARCHY`)**. No supported timeframe exists above `1MO`. See Section 9.3 for exact `1MO` behavior. |

### 9.3 Exact Operation of `1MO` (Monthly) When No Higher Timeframe Exists
Because `1MO` is the ceiling of the nine-timeframe architecture (`1M` through `1MO`), it has **zero higher timeframes (`HTF 1 = NULL`, `HTF 2 = NULL`)**:
1. **Strict Prohibition of LTF-as-HTF Substitution:** `1W` is a lower timeframe relative to `1MO` and must **never** be used as an HTF bias source for `1MO`.
2. **Mode A on `1MO` (`INDEPENDENT_TIMEFRAME`):** Operates identically to Mode A on any other timeframe—evaluates the 11 single-timeframe brains (`Brain 1` and `Brains 3..12`) directly on confirmed `1MO` candles, while Brain 2 is `INACTIVE_IN_MODE_A` (`NEUTRAL`).
3. **Mode B on `1MO` (`MTF_CONFIRMED` Request Handling):**
   - If a user or worker requests `MODE_B_MTF_CONFIRMED` with `execution_timeframe = '1MO'`, the system logs `MTF_TOP_OF_HIERARCHY_NO_HTF_EXISTS`.
   - **Brain 2 (`BRAIN_02_MTF`):** Because no HTF exists above `1MO` to compute higher-timeframe alignment, Brain 2 outputs `vote = 'NEUTRAL'`, `confidence = 0.00`, with status code `TOP_OF_HIERARCHY_NO_HTF` (it does **not** fabricate a fake `BUY`/`SELL` vote and does **not** trigger a missing-data error veto, because the absence of an HTF above `1MO` is a structural boundary of the 9-timeframe specification, not a feed failure).
   - **LTF Confirmation Option on `1MO`:** In Mode B on `1MO`, Phase 3 MTF check verifies that the last closed **`1W` (`LTF`)** candle does not hold an active opposing structural break (`CHoCH`/`MSS`) against the `1MO` signal direction, and active voting consensus is evaluated across the 11 eligible `1MO` brains (`Brain 1` and `Brains 3..12`).

---

## 10. Trading Methodology

QUANTUM implements a **Hybrid Sniper + Fast Scalper** methodology operating under **Confirmed-Only (`STRICT`)** rules.

### 10.1 Sniper Sub-Methodology (Precision Structural Reversal & Continuation)
- **Objective:** Enter at high-probability institutional Points of Interest (POIs) where risk distance (`|Entry - SL|`) is tightly bounded by structural invalidation, yielding asymmetric Risk-to-Reward (`R:R >= 1:2.0` to `1:5.0+`).
- **Setup Sequence:**
  1. **HTF / Dealing Range Context:** Price reaches an institutional POI (unmitigated Order Block, Fair Value Gap, Breaker Block, or Premium/Discount extreme) or sweeps an external/internal liquidity pool (`BSL`/`SSL`, `PDH`/`PDL`, `EQH`/`EQL`).
  2. **Structural Shift & Displacement:** Market prints a confirmed Liquidity Sweep rejection or Change of Character (`CHoCH`) / Market Structure Shift (`MSS`) backed by strong displacement (large candle body + FVG creation).
  3. **Confirmed Trigger:** On the confirmed close of the trigger/retest candle inside or rejecting the Entry Zone, the signal transitions to confirmed `BUY` or `SELL`.
  4. **Invalidation:** Strictly placed beyond the structural swing extreme or sweep wick that anchored the POI plus a market/timeframe-specific volatility/spread buffer.

### 10.2 Fast Scalper Sub-Methodology (Momentum & Displacement Continuation)
- **Objective:** Capture high-velocity directional expansions following confirmed Break of Structure (`BOS`), Fair Value Gap continuation, or session liquidity breakouts.
- **Setup Sequence:**
  1. **Directional Momentum & Session Volume:** Active liquid session (e.g., London or NY open for `XAUUSD`, high-volume expansion for `BTCUSD`) with aligned trend and momentum brains.
  2. **Displacement Breakout / Pullback:** Price confirms a `BOS` with displacement volume and immediately respects a shallow micro-FVG or mitigation block without violating internal structure.
  3. **Confirmed Trigger:** Immediate execution on the confirmed close of the continuation candle with tight structural Stop Loss (using the deterministic Fast Scalper Micro-Impulse Anchor rules defined in Section 15.1) and rapid partial scale-out (`TP1` at `1.0R–1.5R` with automatic Break-Even rule).

---

## 11. Twelve Brains Intelligence Core

The Phase 1 Intelligence Core comprises **12 modular, deterministic analytical brains**.

### 11.1 Mandatory Rules Governing All 12 Brains
1. **Equal Voting Weight:** Every brain holds a voting weight of `1`.
2. **Separation of Vote and Confidence:**
   - `vote`: Enum strictly in `{'BUY', 'SELL', 'NEUTRAL', 'ABSTAIN_DATA_UNAVAILABLE'}`.
   - `confidence`: Float strictly in `[0.00, 100.00]`, measuring signal clarity and strength within that brain's domain. Confidence never multiplies the integer vote count in Equal Voting mode.
3. **Zero Fake Votes on Missing Data:** If required candle history, volume data, or dependent features are missing/corrupted, the brain must output `vote = 'ABSTAIN_DATA_UNAVAILABLE'`, `confidence = 0.0`, and log the exact missing input. It must **never** default to `NEUTRAL` (which implies the market was analyzed and found flat) or fabricate a directional vote.
4. **Orthogonality & Anti-Duplication Rule:** Each brain evaluates a distinct analytical dimension. Two brains must not compute the exact same indicator formula to artificially inflate the vote count for the same underlying evidence.
5. **Market & Timeframe Specific Profiles:** Every brain loads its threshold configuration from a `(symbol, timeframe, strategy_version)` parameter profile.

---

### 11.2 Detailed Specification of Each of the 12 Brains

#### Brain 1: Trend Intelligence (`BRAIN_01_TREND`)
- **Purpose:** Determine the prevailing directional trend regime (Bullish, Bearish, or Ranging/Transitioning) on the active timeframe.
- **Responsibilities:** Evaluate multi-horizon moving average geometry, slope velocity, and directional movement persistence without overlapping with raw oscillator momentum (Brain 9) or swing pivot BOS (Brain 3).
- **Required Inputs:** Confirmed OHLC series, configured Fast/Medium/Slow EMA lengths (standard profile: `21, 50, 200`; `1MO` macro profile: `12, 24, 60` when `< 200` monthly bars exist, as documented in Section 25.4), ADX/DMI(14) period, and ATR(14) for slope normalization.
- **Historical Bar Tiers (`0–199`, `200–249`, and `>= 250` Confirmed Bars):**
  To reconcile exact EMA(200) convergence requirements across unit tests, runtime rules, and acceptance criteria:
  - **Tier 1 (`0 to 199 confirmed bars` on `1M`–`1W`; or `< 60 confirmed bars` on `1MO`):** Hard insufficient history. Returns `vote = 'ABSTAIN_DATA_UNAVAILABLE'`, `confidence = 0.00`, error code `ERR_BRAIN01_INSUFFICIENT_BARS_LT_200`.
  - **Tier 2 (`200 to 249 confirmed bars` — Warm-Up Convergence Window):** `EMA(21)`, `EMA(50)`, `EMA(200)`, `ADX(14)`, and `ATR(14)` are mathematically computable, but `EMA(200)` has not completed its full 50-bar post-seed exponential decay stabilization. Brain 1 executes normally and casts a valid `BUY`, `SELL`, or `NEUTRAL` vote, flags `warmup_status = 'CONVERGING_200_249'`, and applies a deterministic **0.85x warm-up confidence multiplier** (`max confidence = 85.00`).
  - **Tier 3 (`>= 250 confirmed bars` — Full Institutional Convergence):** Full exponential stabilization achieved (`warmup_status = 'FULL_CONVERGENCE_250_PLUS'`); confidence is evaluated across the full `[0.00, 100.00]` range with `1.00x` multiplier.
- **Indicators & Calculations:**
  - EMA Stack Alignment: $\text{EMA}_{\text{fast}} > \text{EMA}_{\text{med}} > \text{EMA}_{\text{slow}}$ (Bullish) vs. inverse (Bearish).
  - Normalized EMA Slope: $\frac{\text{EMA}_{\text{med}}[0] - \text{EMA}_{\text{med}}[k]}{k \cdot \text{ATR}(14)}$.
  - Trend Strength Index: ADX(14) paired with $+DI$ and $-DI$ separation.
- **Analysis Methodology:** Confirms a directional trend only when the EMA stack is aligned, normalized slope exceeds the timeframe's minimum slope threshold, and ADX confirms trend regime rather than low-energy chop.
- **Validation Rules:** Close price and all EMA values must be finite numbers (`> 0`).
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Bullish EMA alignment + positive normalized slope above threshold + $+DI > -DI$ with ADX above trend floor.
  - `SELL`: Bearish EMA alignment + negative normalized slope below threshold + $-DI > +DI$ with ADX above trend floor.
  - `NEUTRAL`: Mixed EMA stack, flat slope, or ADX below trend floor (choppy/sideways market).
- **Confidence Calculation:** Weighted composite (0–100) of EMA stack separation (35%), normalized slope magnitude capped at 2.5 ATR (35%), and ADX directional strength (30%), multiplied by `0.85` if bar count is in `[200, 249]` or `1.00` if `>= 250`.
- **Explanation:** Generates deterministic text, e.g., `"Bullish trend confirmed (260 bars, FULL_CONVERGENCE): EMA(21)>EMA(50)>EMA(200), slope +0.42 ATR/bar, ADX 31.4 (+DI 28.1 > -DI 14.2)."`
- **Timestamp:** ISO-8601 UTC timestamp of the confirmed candle close.
- **Error Handling & Missing-Data Behaviour:** If `< 200` confirmed bars exist (or `< 60` bars on `1MO` macro profile), returns `ABSTAIN_DATA_UNAVAILABLE` with `ERR_BRAIN01_INSUFFICIENT_BARS_LT_200`.
- **Dependencies:** Confirmed OHLCV Ingestion Service.
- **Unit Tests:** Test `< 200` bars (`0–199` $\rightarrow$ `ABSTAIN_DATA_UNAVAILABLE`), `200–249` bars (valid vote + `0.85x` confidence cap), and `>= 250` bars (full confidence `1.00x`) across bullish, bearish, and sideways series.
- **Limitations:** Lagging during sharp V-shaped reversals (compensated by Brains 3, 5, and 6).

---

#### Brain 2: Multi-Timeframe Intelligence (`BRAIN_02_MTF`)
- **Purpose:** Evaluate directional alignment between the selected Execution Timeframe (`T_exec`) and its mapped Higher Timeframes (`HTF 1`, `HTF 2`) using strictly closed HTF candles.
- **Responsibilities:** Synthesize HTF trend bias, HTF structural direction, and HTF dealing-range location into a single directional vote for the active execution timeframe in Mode B, while preserving strict single-timeframe isolation in Mode A.
- **Required Inputs:** `signal_mode` (`INDEPENDENT_TIMEFRAME` | `MTF_CONFIRMED`), confirmed execution timeframe timestamp $t_{\text{exec}}$, and (in Mode B) the most recently **closed** OHLCV and structural summaries of mapped `HTF 1` and `HTF 2` (from Section 9.2) where $t_{\text{htf\_close}} \le t_{\text{exec}}$.
- **Mode-Dependent Execution & Hierarchy Boundary Rules:**
  1. **Mode A (`INDEPENDENT_TIMEFRAME`):** Brain 2 does **not** inject HTF bias into an independent timeframe signal. It returns `vote = 'NEUTRAL'`, `confidence = 0.00`, `mode_status = 'INACTIVE_IN_MODE_A'`, and logs informational HTF telemetry separately without affecting Mode A's 11-brain active directional voting pool.
  2. **Mode B (`MTF_CONFIRMED`) on `1M` through `1D` (2 HTFs exist: `HTF 1` and `HTF 2`):** Evaluates both `HTF 1` (weight 60%) and `HTF 2` (weight 40%).
  3. **Mode B (`MTF_CONFIRMED`) on `1W` (1 HTF exists: `HTF 1 = 1MO`, `HTF 2 = NULL`):** Evaluates `1W` strictly against `1MO` (`100%` of HTF weight assigned to `1MO`; zero duplication).
  4. **Mode B (`MTF_CONFIRMED`) on `1MO` (0 HTFs exist: `HTF 1 = NULL`, `HTF 2 = NULL`):** Because no timeframe exists above `1MO`, Brain 2 returns `vote = 'NEUTRAL'`, `confidence = 0.00`, `mode_status = 'TOP_OF_HIERARCHY_NO_HTF'`. It never substitutes a lower timeframe (`1W`) as an HTF.
- **Indicators & Calculations (Mode B when $\ge 1$ HTF exists):**
  - `HTF 1` and `HTF 2` confirmed structure state (`BULLISH`, `BEARISH`, `RANGING`).
  - `HTF 1` and `HTF 2` candle body direction, EMA(50) bias, and Premium/Discount dealing range location on last closed HTF candle.
  - Alignment Concordance Score across `[T_exec, HTF_1, HTF_2]`.
- **Analysis Methodology:** Strictly enforces the **Non-Repainting HTF Cutoff Rule**: an in-progress HTF candle is ignored until its close timestamp satisfies $t_{\text{htf\_close}} \le t_{\text{exec}}$.
- **Validation Rules:** Assert `htf_candle.close_time <= exec_candle.close_time`. Any violation raises `LookaheadBiasException`.
- **BUY / SELL / NEUTRAL Output (Mode B):**
  - `BUY`: Both `HTF 1` and `HTF 2` hold confirmed bullish bias/structure (or `HTF 1` is confirmed bullish while `HTF 2` is in a confirmed bullish discount pullback; on `1W`, `HTF 1 = 1MO` is confirmed bullish).
  - `SELL`: Both `HTF 1` and `HTF 2` hold confirmed bearish bias/structure (or `HTF 1` is confirmed bearish while `HTF 2` is in a confirmed bearish premium pullback; on `1W`, `HTF 1 = 1MO` is confirmed bearish).
  - `NEUTRAL`: Mode A is active, OR `T_exec == 1MO`, OR `HTF 1` and `HTF 2` are in direct conflict (`HTF 1` Bullish vs. `HTF 2` Bearish).
- **Confidence Calculation:** In Mode B with 2 HTFs: `HTF 1` alignment (60%) + `HTF 2` alignment (40%) scaled by HTF displacement strength (`0–100`). In Mode B on `1W`: `100%` derived from `1MO` alignment and displacement. In Mode A or `1MO`: `0.00`.
- **Explanation:** E.g., `"Mode B 15M execution aligned with confirmed 1H Bullish BOS (closed 14:00 UTC) and 4H Bullish trend (closed 12:00 UTC)."`
- **Timestamp:** Execution candle close UTC + referenced HTF close UTC timestamps.
- **Error Handling & Missing-Data Behaviour:** In Mode B (for `1M`–`1W`), if a required mapped HTF data stream is stale or unavailable, returns `ABSTAIN_DATA_UNAVAILABLE` (`ERR_BRAIN02_HTF_MISSING`), which triggers a Gate 3/Gate 5 `WAIT` decision in Mode B.
- **Dependencies:** Phase 3 MTF Synchronization Service & Phase 2 SMC Structure Interface.
- **Unit Tests:** Verify timestamp boundary enforcement (`14:15 UTC` 15M bar uses `13:00–14:00 UTC` closed 1H bar), verify Mode A returns `NEUTRAL` (`INACTIVE_IN_MODE_A`), verify `1W` uses single HTF (`1MO`), and verify `1MO` outputs `TOP_OF_HIERARCHY_NO_HTF` without using `1W` as HTF.
- **Limitations:** Cannot evaluate timeframes above `1MO` as none are part of the 9-timeframe specification.

---

#### Brain 3: Market Structure (`BRAIN_03_STRUCTURE`)
- **Purpose:** Track institutional market structure via confirmed Swing Highs/Lows, Higher Highs (`HH`), Higher Lows (`HL`), Lower Highs (`LH`), Lower Lows (`LL`), Break of Structure (`BOS`), Change of Character (`CHoCH`), and Market Structure Shift (`MSS`).
- **Responsibilities:** Maintain dual-layer structural state (Internal Structure for tactical shifts; External Structure for major dealing-range trend).
- **Required Inputs:** Confirmed OHLC series, timeframe-specific pivot lookback lengths (`internal_pivot_len`, `external_pivot_len`), and minimum body-close breakout threshold.
- **Indicators & Calculations:**
  - Confirmed Fractal Pivot Highs/Lows (verified after `rightBars` confirmed closes).
  - Body Close Verification: A valid `BOS` or `CHoCH` requires a confirmed candle **body close** (`close > swing_high` or `close < swing_low`), not merely a wick penetration (which is classified as a sweep by Brain 5).
- **Analysis Methodology:** Tracks sequence of external and internal swings. Distinguishes trend continuation (`BOS`) from trend reversal (`CHoCH` / `MSS`).
- **Validation Rules:** Pivot timestamps must be strictly chronological; swing high must be `> swing low`.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Confirmed Bullish External `BOS` with intact Higher Low, or confirmed Bullish `MSS`/`CHoCH` following protected low.
  - `SELL`: Confirmed Bearish External `BOS` with intact Lower High, or confirmed Bearish `MSS`/`CHoCH` following protected high.
  - `NEUTRAL`: Price compressed inside internal range with contradicting internal/external breaks or unconfirmed wick-only violation.
- **Confidence Calculation:** Derived from external + internal structural agreement (50%), distance from protected structural invalidation level (25%), and breakout candle body displacement above the broken pivot (25%).
- **Explanation:** E.g., `"External & Internal Structure Bullish: Confirmed 15M Bullish BOS via body close at 2654.20 above prior Swing High 2651.80; Protected HL at 2644.10."`
- **Timestamp:** Confirmed candle close UTC.
- **Error Handling & Missing-Data Behaviour:** Returns `ABSTAIN_DATA_UNAVAILABLE` if insufficient bars exist to establish at least 4 confirmed external swing pivots.
- **Dependencies:** Phase 2 SMC Structure Module (`ISMCStateProvider`).
- **Unit Tests:** Test wick-only break (must NOT trigger BOS), body-close break (triggers BOS), and CHoCH transition from LH/LL to HH/HL.
- **Limitations:** Requires `rightBars` confirmation for new swing pivots, deliberately trading earliest possible pivot guesswork for non-repainting certainty.

---

#### Unified Liquidity Pool Lifecycle State Machine (Shared by Brain 4 & Brain 5)

To eliminate any timing contradiction between **Brain 4 (`Liquidity Mapping`)** and **Brain 5 (`Liquidity Sweep`)** when a candle breaches a liquidity pool, both brains read from a single deterministic **7-State Liquidity Pool Lifecycle Machine** evaluated in strict sequence on every confirmed candle close $t$:

```
[1. CREATED] ──(Confirmed pivot/session close)──► [2. ACTIVE_UNMITIGATED]
                                                            │
                        ┌───────────────────────────────────┴───────────────────────────────────┐
                        │ (Candle t breaches level: High > BSL or Low < SSL)                    │ (Age > max_pool_age_bars)
                        ▼                                                                       ▼
            [3. RAIDED_UNDER_EVALUATION]                                                  [7. EXPIRED]
                        │
        ┌───────────────┼───────────────┐
        │               │               │
  (1-bar reclaim   (Candle t closes   (Candle t or t+1 closes
   close inside     marginally out;    decisively beyond level
   on bar t)        await bar t+1)     with body displacement)
        │               │               │
        ▼               ▼               ▼
 [4. SWEPT_RECLAIMED] ◄─┘      [5. INVALIDATED_BROKEN_BOS]
 (Active for sweep_expiry_bars)         │
        │                               ▼
        └──────────────────────► [6. CONSUMED_ARCHIVED]
```

| Lifecycle State | Exact Transition Rule | Brain 4 (`Liquidity Mapping`) Behavior | Brain 5 (`Liquidity Sweep`) Behavior |
| :--- | :--- | :--- | :--- |
| **1. `CREATED`** | Swing pivot completes $k$ right-hand confirmation bars, or Session / `PDH`/`PDL` / `PWH`/`PWL` boundary closes. | Validates pool coordinates and promotes immediately to `ACTIVE_UNMITIGATED`. | No sweep yet (`NEUTRAL`). |
| **2. `ACTIVE_UNMITIGATED`** | Resting liquidity level has never been breached (`High <= BSL` or `Low >= SSL`) since creation. | **Eligible Magnet Target:** Brain 4 actively uses this pool to compute the upward/downward **Draw on Liquidity**. | Monitors this pool as an eligible sweep candidate. |
| **3. `RAIDED_UNDER_EVALUATION`** | On confirmed bar $t$, `High_t > BSL` or `Low_t < SSL` by penetration depth $d_{\text{sweep}} \in [d_{\text{min}}, d_{\text{max\_atr}}]$. | Immediately removes the pool from future magnet targets (since its resting stops have just been triggered). | Evaluates bar $t$ for 1-bar reclaim (`Close_t < BSL` or `Close_t > SSL`) or holds for bar $t+1$ (2-bar reclaim window). |
| **4. `SWEPT_RECLAIMED`** | Bar $t$ (1-bar SFP) or bar $t+1$ (2-bar reclaim) closes firmly back inside the swept level with rejection ratio $\ge \theta_{\text{wick}}$. | Pool is marked swept; Brain 4 redirects the Draw on Liquidity toward the **opposing** `ACTIVE_UNMITIGATED` pool across the range. | **Active Sweep Signal:** Brain 5 outputs `BUY` (for `SSL` sweep reclaim) or `SELL` (for `BSL` sweep reclaim) for `sweep_expiry_bars` (e.g., 3 bars) unless invalidated. |
| **5. `INVALIDATED_BROKEN_BOS`** | Penetration exceeds $d_{\text{max\_atr}}$ OR bar $t$ / $t+1$ closes beyond the sweep extreme as a continuation breakout (`BOS`). | Pool is broken; Brain 4 maps the next higher/lower external pool. | Sweep rejected/invalidated; Brain 5 outputs `NEUTRAL` (Brain 3 handles the `BOS`). |
| **6. `CONSUMED_ARCHIVED`** | `SWEPT_RECLAIMED` window (`sweep_expiry_bars`) elapses, or trade plan from the sweep completes. | Archived in historical `smc_analyses` ledger. | Sweep recency window expired; Brain 5 returns to `NEUTRAL`. |
| **7. `EXPIRED`** | An untouched minor internal pool exceeds `max_pool_age_bars` without interaction. | Pruned from active magnet weighting. | Ignored. |

---

#### Brain 4: Liquidity Mapping (`BRAIN_04_LIQUIDITY_MAP`)
- **Purpose:** Map resting `ACTIVE_UNMITIGATED` Buy-Side Liquidity (`BSL`) and Sell-Side Liquidity (`SSL`) pools acting as price magnets (draw on liquidity).
- **Responsibilities:** Identify where untouched resting stop orders and institutional liquidity pools reside—including Equal Highs (`EQH`), Equal Lows (`EQL`), Old Swing Highs/Lows, Previous Day High/Low (`PDH`/`PDL`), Previous Week High/Low (`PWH`/`PWL`), and Asian/London/NY Session Highs/Lows—and determine the active **Draw on Liquidity**.
- **Required Inputs:** Confirmed OHLCV series, timezone-aware session/daily/weekly highs and lows, ATR(14), and the Unified Liquidity Pool Registry (`Phase 2`).
- **Indicators & Calculations:**
  - Liquidity Pool Clustering: Groups `ACTIVE_UNMITIGATED` swing highs/lows within $\pm \alpha \cdot \text{ATR}$ into `EQH`/`EQL` pools.
  - Liquidity Density & Proximity Score: Ranks `ACTIVE_UNMITIGATED` pools by age, number of touches without violation, and structural significance (`PWH/PWL > PDH/PDL > Session High/Low > Internal EQH/EQL`).
  - Post-Sweep Draw Reversal Vector: When an `SSL` pool transitions to `SWEPT_RECLAIMED`, Brain 4 immediately scores the draw vector upward toward the nearest opposing `ACTIVE_UNMITIGATED` `BSL` pool (and vice versa).
- **Analysis Methodology:** Determines whether the dominant draw on liquidity is upward toward resting `ACTIVE_UNMITIGATED` `BSL` or downward toward resting `ACTIVE_UNMITIGATED` `SSL`, provided sufficient clear space (R:R room) exists before hitting opposing hurdle liquidity.
- **Validation Rules:** Only pools in state `ACTIVE_UNMITIGATED` can serve as future magnet targets (`TP1`/`TP2`/`TP3`). When a pool is breached on bar $t$, it transitions to `RAIDED_UNDER_EVALUATION` / `SWEPT_RECLAIMED` (never deleted), remaining fully accessible to Brain 5 on the exact same bar $t$ and for `sweep_expiry_bars`.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Clear `ACTIVE_UNMITIGATED` `BSL` target pool above current price with asymmetric distance relative to nearest downside `SSL` threat (especially when expanding away from a `SWEPT_RECLAIMED` `SSL` pool or Discount POI).
  - `SELL`: Clear `ACTIVE_UNMITIGATED` `SSL` target pool below current price with asymmetric distance relative to nearest upside `BSL` threat (especially when expanding away from a `SWEPT_RECLAIMED` `BSL` pool or Premium POI).
  - `NEUTRAL`: Equidistant between major `BSL` and `SSL` pools (equilibrium chop) or immediately capped by an adjacent `ACTIVE_UNMITIGATED` liquidity pool blocking expansion.
- **Confidence Calculation:** Function of target liquidity significance weight (40%), number of clustered equal highs/lows (30%), and clear spatial path-to-target ratio (30%).
- **Explanation:** E.g., `"Draw on Liquidity is Bullish toward ACTIVE_UNMITIGATED EQH + PDH BSL pool at 2668.50 (+14.20 pts clear range) following SSL reclaim."`
- **Timestamp:** Confirmed candle close UTC.
- **Error Handling & Missing-Data Behaviour:** If session/daily reference candles are missing, returns `ABSTAIN_DATA_UNAVAILABLE`.
- **Dependencies:** Phase 2 Unified Liquidity Pool Registry (`ISMCStateProvider`).
- **Unit Tests:** Test EQH clustering, verify transition from `ACTIVE_UNMITIGATED` $\rightarrow$ `RAIDED_UNDER_EVALUATION` $\rightarrow$ `SWEPT_RECLAIMED` preserves the pool object for Brain 5 on the same bar, and test DST-aware PDH/PDL rollover.
- **Limitations:** Infers resting liquidity from price geometry and session highs/lows rather than proprietary central-bank Level-3 order books.

---

#### Brain 5: Liquidity Sweep (`BRAIN_05_LIQUIDITY_SWEEP`)
- **Purpose:** Detect completed stop-runs / liquidity raids (Turtle Soups / SFP — Swing Failure Patterns) where price pierces a resting `BSL` or `SSL` pool and closes back inside the prior structural range.
- **Responsibilities:** Differentiate between a genuine structural breakout (`BOS`, handled by Brain 3) and a liquidity sweep / stop-hunt rejection (`SWEPT_RECLAIMED`).
- **Required Inputs:** Pools in states `ACTIVE_UNMITIGATED`, `RAIDED_UNDER_EVALUATION`, and `SWEPT_RECLAIMED` from the Unified Liquidity Pool Registry, confirmed candle OHLC, volume, and ATR(14).
- **Indicators & Calculations:**
  - Sweep Penetration Depth: $d_{\text{sweep}} = \text{High} - \text{BSL}$ (for bearish sweep) or $\text{SSL} - \text{Low}$ (for bullish sweep).
  - Wick-to-Range Rejection Ratio: $\frac{\text{Rejection Wick Length}}{\text{Total Candle Range}}$.
  - Reclaim Verification: Candle `close < BSL` (after `high > BSL`) or `close > SSL` (after `low < SSL`) within $N \in [1, 2]$ confirmed candles, transitioning the pool state from `RAIDED_UNDER_EVALUATION` to `SWEPT_RECLAIMED`.
- **Analysis Methodology:** Inspects any pool that entered `RAIDED_UNDER_EVALUATION` on bar $t$ or bar $t-1$, or currently sits in `SWEPT_RECLAIMED` within its recency window (`bars_since_reclaim < sweep_expiry_bars`, default 3 bars) provided the sweep extreme wick has not been violated.
- **Validation Rules:** Penetration depth must satisfy $d_{\text{min}} \le d_{\text{sweep}} \le d_{\text{max\_atr}}$ and sweep extreme must remain intact (`Low >= sweep_extreme_low` for bullish sweep; `High <= sweep_extreme_high` for bearish sweep).
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Pool is in confirmed `SWEPT_RECLAIMED` state for an `SSL` raid (`EQL`, `PDL`, Session Low, or Swing Low) within the active `sweep_expiry_bars` window with sweep low intact.
  - `SELL`: Pool is in confirmed `SWEPT_RECLAIMED` state for a `BSL` raid (`EQH`, `PDH`, Session High, or Swing High) within the active `sweep_expiry_bars` window with sweep high intact.
  - `NEUTRAL`: No pool in `SWEPT_RECLAIMED` within `sweep_expiry_bars`, or price closed beyond the sweep level as `INVALIDATED_BROKEN_BOS`.
- **Confidence Calculation:** Weighted by significance of the swept liquidity pool (40%), rejection wick ratio (35%), and reclaim close strength / recency decay (25%).
- **Explanation:** E.g., `"Bullish SSL Sweep (State: SWEPT_RECLAIMED, bar 1 of 3): London Low (2638.00) raided to 2636.85 and reclaimed with confirmed close at 2641.20 (wick rejection ratio 0.72)."`
- **Timestamp:** Confirmed candle close UTC + sweep event timestamp.
- **Error Handling & Missing-Data Behaviour:** Returns `ABSTAIN_DATA_UNAVAILABLE` if the Unified Liquidity Pool Registry is uninitialized or unavailable.
- **Dependencies:** Unified Liquidity Pool Registry (`Phase 2`) shared with Brain 4.
- **Unit Tests:** Test simultaneous same-bar execution of Brain 4 and Brain 5 on a 1-bar SFP sweep (verifying Brain 4 shifts draw target while Brain 5 emits `BUY`/`SELL` without any missing-pool conflict), 2-bar sweep reclaim, and `INVALIDATED_BROKEN_BOS`.
- **Limitations:** Deep news-driven spikes can exceed $d_{\text{max\_atr}}$; handled in tandem with Phase 6 News Protection.

---

#### Brain 6: Reversal and Trap Detection (`BRAIN_06_REVERSAL_TRAP`)
- **Purpose:** Identify institutional inducement traps, retail breakout traps (bull traps / bear traps), and momentum exhaustion divergences at structural extremes.
- **Responsibilities:** Detect when retail traders are induced into taking the wrong side of the market prior to an institutional reversal, or warn against entering a late chasing signal into exhaustion.
- **Required Inputs:** Confirmed OHLCV series, Internal Inducement (`IDM`) pivots, RSI/Momentum series, and Volume/Range compression metrics.
- **Indicators & Calculations:**
  - Inducement (`IDM`) Trap Detection: Raid of the first minor internal pullback pivot after a `BOS` that traps early counter-trend or late breakout participants before tapping the true POI.
  - Multi-Bar False Breakout Trap: Candle $t-1$ closes marginally beyond a minor range high/low with declining volume/follow-through, and candle $t$ engulfs and closes back inside in the opposite direction.
  - Structural Exhaustion Divergence: Price prints a marginal new extreme inside an HTF POI while momentum/displacement velocity contracts sharply across consecutive swings.
- **Analysis Methodology:** Evaluates trap signatures both positively (confirming an institutional reversal after a bear/bull trap has sprung) and defensively (casting a counter-vote when the current move is a low-displacement trap).
- **Validation Rules:** All divergence and engulfing patterns require confirmed candle close.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Confirmed Bear Trap / Bullish Inducement sweep & engulfing reversal at discount support.
  - `SELL`: Confirmed Bull Trap / Bearish Inducement sweep & engulfing reversal at premium resistance.
  - `NEUTRAL`: No active trap or reversal signature present.
- **Confidence Calculation:** Composite of engulfing body ratio (40%), inducement structural location (35%), and exhaustion divergence slope (25%).
- **Explanation:** E.g., `"Bearish Bull-Trap confirmed: Minor breakout above 89,800 failed on contracting displacement and was immediately engulfed by confirmed bearish close at 89,320."`
- **Timestamp:** Confirmed candle close UTC.
- **Error Handling & Missing-Data Behaviour:** Returns `ABSTAIN_DATA_UNAVAILABLE` if OHLCV history is shorter than required divergence lookback.
- **Dependencies:** Phase 2 Inducement & Structure Module (`ISMCStateProvider`).
- **Unit Tests:** Test bull trap engulfing pattern, bear trap engulfing pattern, and clean breakout (must not falsely flag as trap when displacement is expanding).
- **Limitations:** Early counter-trend divergence in a parabolic runaway market can fail if used alone; mitigated by requiring Equal Voting consensus across all 12 brains in `STRICT` mode.

---

#### Brain 7: Order Block Analysis (`BRAIN_07_ORDER_BLOCK`)
- **Purpose:** Detect, validate, track mitigation of, and score institutional **Order Blocks (`OB`)**, **Breaker Blocks (`BB`)**, and **Mitigation Blocks (`MB`)**.
- **Responsibilities:** Maintain a deterministic, non-contradictory lifecycle registry of valid bullish and bearish institutional blocks and evaluate price interaction at those zones.
- **Required Inputs:** Confirmed OHLCV series, confirmed `BOS`/`MSS` events, displacement metrics, and FVG registry from `ISMCStateProvider`.
- **Order Block Geometry Definitions:**
  - **Bullish Order Block:** The last down-close candle immediately preceding an upward displacement impulse that creates an `FVG` and breaks structure (`BOS`/`MSS`).
    - `Proximal Edge` = Candle `High` (or upper body edge).
    - `Mean Threshold (MT, 50%)` = $\frac{\text{Proximal} + \text{Distal}}{2}$.
    - `Distal Edge (Hard Invalidation Boundary)` = Candle `Low`.
  - **Bearish Order Block:** The last up-close candle immediately preceding a downward displacement impulse that creates an `FVG` and breaks structure (`BOS`/`MSS`).
    - `Proximal Edge` = Candle `Low` (or lower body edge).
    - `Mean Threshold (MT, 50%)` = $\frac{\text{Proximal} + \text{Distal}}{2}$.
    - `Distal Edge (Hard Invalidation Boundary)` = Candle `High`.
- **Authoritative Distinction Between Mitigation, Invalidation, and Breaker Conversion (Unified 6-State OB Lifecycle):**
  1. **`UNMITIGATED_FRESH`:** OB is newly confirmed by `BOS`/`MSS` + `FVG`; price has not yet returned to touch its `Proximal Edge`.
  2. **`MITIGATED_SHALLOW_ACTIVE` (First Touch / Respect Above MT):** Price retraces into `[MT, Proximal]` (wick or close enters the upper half of a Bullish OB or lower half of a Bearish OB) and prints a confirmed rejection close without any candle **body close** violating the `50% Mean Threshold (MT)`. **Status:** Valid, highest-conviction active entry state (`MT_Respected_Score = 100%`).
  3. **`MITIGATED_DEEP_ACTIVE` (Deep Touch / Body Below MT, Distal Intact):** Price penetrates deeper than `50% MT` (or closes inside `(Distal, MT)`), **but** candle **body close** remains strictly inside the **`Distal Edge`** (`Close >= Distal_Low` for Bullish OB; `Close <= Distal_High` for Bearish OB). **Status:** The OB is **NOT invalidated** (unless the user explicitly enables an optional `strict_mt_invalidation = TRUE` override in Strategy Lab); it remains active for reaction on that retest, but its `MT_Respected_Score` is penalized to `0%` (reducing Brain 7 confidence by 30 points), and after price expands away (`> 1.0 ATR`) from a first mitigation tap, the OB transitions to `MITIGATED_CONSUMED`.
  4. **`MITIGATED_CONSUMED`:** Price has tapped the OB (`SHALLOW` or `DEEP`) and expanded away by $\ge 1.5 \times \text{ATR}(14)$ toward target. Its institutional resting orders are considered filled; subsequent touches do not trigger new Sniper entries.
  5. **`INVALIDATED` (Hard Distal Close Violation):** A confirmed candle **body close** violates the **`Distal Edge`** (`Close < Distal_Low` for Bullish OB; `Close > Distal_High` for Bearish OB). Once `INVALIDATED`, the zone can **never** generate same-direction OB votes again.
  6. **`CONVERTED_TO_BREAKER_BLOCK` (`BB`) or `MITIGATION_BLOCK` (`MB`):** When an OB transitions to `INVALIDATED` via an impulsive opposing displacement candle (`DR >= 1.25`) that causes an opposing `MSS`:
     - If the failed OB had formed immediately after a **Liquidity Sweep** (or swept a prior swing extreme before failing), it converts into a **`BREAKER_BLOCK` (`BB`)** of opposite polarity.
     - If the failed OB formed during a failure swing that did **not** sweep the prior swing extreme before failing, it converts into a **`MITIGATION_BLOCK` (`MB`)** of opposite polarity.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Price taps a Bullish OB (or Bullish `BB`/`MB`) transitioning from `UNMITIGATED_FRESH` into `MITIGATED_SHALLOW_ACTIVE` (or `MITIGATED_DEEP_ACTIVE` with confirmed rejection close holding `Close >= Distal_Low`) in Discount/Equilibrium.
  - `SELL`: Price taps a Bearish OB (or Bearish `BB`/`MB`) transitioning from `UNMITIGATED_FRESH` into `MITIGATED_SHALLOW_ACTIVE` (or `MITIGATED_DEEP_ACTIVE` with confirmed rejection close holding `Close <= Distal_High`) in Premium/Equilibrium.
  - `NEUTRAL`: Price is not interacting with an active OB/BB/MB, or the zone was `INVALIDATED` by a distal body close, or the zone is already `MITIGATED_CONSUMED`.
- **Confidence Calculation:**
  - Base Freshness (`UNMITIGATED_FRESH` first touch = 35 pts; `BB`/`MB` first retest = 30 pts).
  - Origin Quality (coupled FVG + liquidity sweep at origin = 35 pts).
  - Mean Threshold Precision (`MITIGATED_SHALLOW_ACTIVE` holding 50% MT = 30 pts; `MITIGATED_DEEP_ACTIVE` violating MT with body close but holding Distal Edge = 0 pts).
- **Explanation:** E.g., `"Bullish Order Block [2640.50 - 2643.00, MT: 2641.75] in MITIGATED_SHALLOW_ACTIVE state on first tap; 50% MT respected (Close 2642.40 >= MT), Confidence 94.0%."`
- **Timestamp:** Confirmed candle close UTC + OB origin candle timestamp.
- **Error Handling & Missing-Data Behaviour:** Returns `ABSTAIN_DATA_UNAVAILABLE` if structural/displacement prerequisites cannot be computed due to missing bars.
- **Dependencies:** Phase 2 SMC Engine (`ISMCStateProvider`).
- **Unit Tests:** Test all 6 states: (1) creation on BOS+FVG, (2) shallow touch holding 50% MT (full confidence), (3) deep touch below 50% MT but holding Distal Edge (remains active with -30pt confidence penalty), (4) consumed after 1.5 ATR expansion, (5) hard invalidation on Distal Edge body close, and (6) conversion to `BB` (with prior sweep) vs. `MB` (without prior sweep).
- **Limitations:** Unfiltered candle coloring creates too many fake OBs; QUANTUM strictly restricts OBs to those that caused a structural break and displacement imbalance.

---

#### Brain 8: Fair Value Gap (`BRAIN_08_FVG`)
- **Purpose:** Identify 3-candle price delivery imbalances—**Bullish Fair Value Gaps (`BISI`)**, **Bearish Fair Value Gaps (`SIBI`)**, and **Inverse Fair Value Gaps (`IFVG`)**—and evaluate rebalance/retest behavior.
- **Responsibilities:** Track open, partially filled, consequent-encroachment (`CE` 50% midpoint) respected, and inverted Fair Value Gaps.
- **Required Inputs:** Confirmed 3-candle sequences $(C_{t-2}, C_{t-1}, C_t)$ and ATR(14).
- **Indicators & Calculations:**
  - **Bullish FVG (`BISI`):** Exists when $\text{Low}_t > \text{High}_{t-2}$ with an impulsive bullish middle candle $C_{t-1}$. Gap zone: $[\text{Distal}=\text{High}_{t-2}, \text{Proximal}=\text{Low}_t]$.
  - **Bearish FVG (`SIBI`):** Exists when $\text{High}_t < \text{Low}_{t-2}$ with an impulsive bearish middle candle $C_{t-1}$. Gap zone: $[\text{Proximal}=\text{High}_t, \text{Distal}=\text{Low}_{t-2}]$.
  - **Consequent Encroachment (`CE`):** Exact 50% midpoint of the FVG: $\text{CE} = \frac{\text{Upper} + \text{Lower}}{2}$.
  - **Inverse FVG (`IFVG`):** When an FVG is impulsively disrespected via a confirmed candle body close completely through its distal boundary ($\text{Close} < \text{High}_{t-2}$ for Bullish FVG; $\text{Close} > \text{Low}_{t-2}$ for Bearish FVG), its polarity inverts into an active IFVG support/resistance zone.
- **Analysis Methodology:** Filters out micro noise gaps smaller than `min_fvg_atr_ratio * ATR(14)`. Tracks price rebalancing into active FVGs or retesting newly inverted IFVGs.
- **Validation Rules:** FVG creation is finalized only on the confirmed close of candle $C_t$.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Price rebalances into an active Bullish FVG (or retests a confirmed Bullish IFVG) and closes above the distal lower boundary (receiving maximum confidence when holding above Consequent Encroachment `CE`), OR creates a fresh breakaway Bullish FVG during a Fast Scalper continuation.
  - `SELL`: Price rebalances into an active Bearish FVG (or retests a confirmed Bearish IFVG) and closes below the distal upper boundary (receiving maximum confidence when holding below `CE`), OR creates a fresh breakaway Bearish FVG during a Fast Scalper continuation.
  - `NEUTRAL`: No active FVG interaction or FVG invalidated without clean IFVG retest.
- **Confidence Calculation:** Function of FVG size relative to ATR (30%), respect of the 50% Consequent Encroachment level (40%), and overlap with Premium/Discount or OB confluence (30%).
- **Explanation:** E.g., `"Bullish FVG [2645.10 - 2648.30, CE: 2646.70] rebalanced and respected with confirmed candle close at 2647.85 above CE."`
- **Timestamp:** Confirmed candle close UTC + FVG 3rd-candle close timestamp.
- **Error Handling & Missing-Data Behaviour:** If an unexpected missing-candle data gap exists inside $(C_{t-2}, C_{t-1}, C_t)$, suppresses false gap detection and logs `GAP_BOUNDARY_SKIPPED`.
- **Dependencies:** Phase 2 SMC Imbalance Module (`ISMCStateProvider`).
- **Unit Tests:** Test Bullish FVG, Bearish FVG, CE 50% calculation, complete fill invalidation, and IFVG polarity inversion.
- **Limitations:** Weekend or daily rollover gaps must be distinguished from 3-candle intraday liquidity voids.

---

#### Brain 9: Momentum Intelligence (`BRAIN_09_MOMENTUM`)
- **Purpose:** Measure directional velocity, acceleration, and momentum regime alignment without duplicating the moving-average stack of Brain 1.
- **Responsibilities:** Evaluate whether internal price momentum supports directional continuation or confirms a structural turn out of an oversold/overbought POI.
- **Required Inputs:** Confirmed OHLC series, timeframe-specific RSI period, MACD/Momentum Oscillator parameters, and Rate of Change (`ROC`) normalized by volatility.
- **Indicators & Calculations:**
  - Regime-Shifted RSI(14): Bullish momentum regime ($50 \le \text{RSI} \le 75$ or sharp hook upward crossing above 40/50 from a POI) vs. Bearish momentum regime ($25 \le \text{RSI} \le 50$ or sharp hook downward crossing below 60/50).
  - Volatility-Normalized ROC: $\text{NROC} = \frac{\text{Close}_t - \text{Close}_{t-n}}{\text{ATR}(14) \cdot \sqrt{n}}$.
  - Impulse Histogram Acceleration: $\Delta H_t = H_t - H_{t-1}$ where $H_t$ is the momentum oscillator histogram.
- **Analysis Methodology:** Avoids naive retail "overbought = sell / oversold = buy" traps during strong trends. Instead, evaluates momentum thrust alignment with structural direction and flags exhaustion when $\text{RSI} > 80$ (blocks late `BUY` chasing) or $\text{RSI} < 20$ (blocks late `SELL` chasing).
- **Validation Rules:** All oscillator inputs must have completed warm-up periods.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Positive NROC above threshold + expanding bullish histogram impulse + RSI in constructive bullish zone (not extreme exhausted $>80$).
  - `SELL`: Negative NROC below threshold + expanding bearish histogram impulse + RSI in constructive bearish zone (not extreme exhausted $<20$).
  - `NEUTRAL`: Flat oscillator momentum near zero-line, conflicting ROC/Histogram direction, or extreme overextended exhaustion warning against late entry.
- **Confidence Calculation:** Derived from NROC magnitude (40%), histogram acceleration consistency over last 3 bars (35%), and RSI regime positioning (25%).
- **Explanation:** E.g., `"Bullish momentum expansion: Normalized ROC +1.35, RSI(14) at 61.8 rising above 50 midline, positive histogram acceleration."`
- **Timestamp:** Confirmed candle close UTC.
- **Error Handling & Missing-Data Behaviour:** Returns `ABSTAIN_DATA_UNAVAILABLE` if fewer than 100 confirmed candles are available (`>= 35` bars on `1MO`).
- **Dependencies:** Confirmed OHLCV Ingestion Service.
- **Unit Tests:** Test momentum expansion, flat equilibrium (`NEUTRAL`), and extreme exhaustion guard ($\text{RSI} > 82$ preventing late `BUY`).
- **Limitations:** Oscillators compress during tight consolidations prior to expansion.

---

#### Brain 10: Volume and Displacement (`BRAIN_10_VOLUME_DISPLACEMENT`)
- **Purpose:** Verify institutional participation through candle displacement kinematics and relative volume (`RVOL`) expansion.
- **Responsibilities:** Distinguish high-conviction institutional order-flow sponsorship from low-volume retail drift, and enforce non-inflated confidence scoring or mandatory abstention when volume is unavailable.
- **Required Inputs:** Confirmed OHLCV series, Volume (tick volume or exchange spot volume), ATR(14), and market/strategy volume policy flag `require_volume_data` (`TRUE` by default for `BTCUSD` and Fast Scalper mode; configurable for `XAUUSD` OTC feeds).
- **Indicators & Calculations:**
  - **Displacement Ratio (`DR`):** $\text{DR}_t = \frac{|\text{Close}_t - \text{Open}_t|}{\text{ATR}(14)}$, scored on $[0, 100]$ via $S_{\text{DR}} = \min\left(100, \max\left(0, \frac{\text{DR}_t - 0.50}{2.00 - 0.50} \times 100\right)\right)$.
  - **Body-to-Range Efficiency (`BRE`):** $\text{BRE}_t = \frac{|\text{Close}_t - \text{Open}_t|}{\text{High}_t - \text{Low}_t}$, scored on $[0, 100]$ via $S_{\text{BRE}} = \min\left(100, \max\left(0, \frac{\text{BRE}_t - 0.40}{0.95 - 0.40} \times 100\right)\right)$.
  - **Relative Volume (`RVOL`):** $\text{RVOL}_t = \frac{\text{Volume}_t}{\text{SMA}(\text{Volume}, 20)}$, scored on $[0, 100]$ via $S_{\text{RVOL}} = \min\left(100, \max\left(0, \frac{\text{RVOL}_t - 0.80}{2.50 - 0.80} \times 100\right)\right)$.
- **Missing-Volume Rules, Abstention Conditions, and Anti-Inflation Confidence Formula:**
  1. **When Brain 10 MUST Abstain (`ABSTAIN_DATA_UNAVAILABLE`):**
     - If `ATR(14) <= 0`, `High <= Low`, or fewer than 20 confirmed bars exist.
     - For **`BTCUSD`** (where true exchange volume is always required) OR whenever `require_volume_data == TRUE` (including all **Fast Scalper** evaluations): if `Volume <= 0`, `Volume IS NULL`, or `SMA(Volume, 20) <= 0`, Brain 10 **must immediately output `vote = 'ABSTAIN_DATA_UNAVAILABLE'` and `confidence = 0.00`** (`ERR_BRAIN10_VOLUME_MISSING`).
  2. **Degraded Price-Only Displacement Mode (`XAUUSD` Sniper Mode Only when `require_volume_data == FALSE` and provider omits tick volume):**
     - To **prevent missing volume data from ever artificially increasing confidence** (which would occur if the 30% RVOL weight were re-normalized onto high price displacement), the missing volume component is assigned **$S_{\text{RVOL}} = 0.00$** (zero points for the 30% volume slot) and the brain's maximum achievable confidence is **hard-capped at `70.00%`**:
       $$C_{\text{with\_volume}} = 0.40 \cdot S_{\text{DR}} + 0.30 \cdot S_{\text{BRE}} + 0.30 \cdot S_{\text{RVOL}} \in [0.00, 100.00]$$
       $$C_{\text{missing\_volume}} = 0.40 \cdot S_{\text{DR}} + 0.30 \cdot S_{\text{BRE}} + 0.30 \cdot (0.00) \in [0.00, 70.00]$$
     - Furthermore, in Degraded Price-Only Mode, casting a directional `BUY` or `SELL` vote requires a stricter displacement threshold ($\text{DR}_t \ge 1.50$ and $\text{BRE}_t \ge 0.75$, compared to $\text{DR}_t \ge 1.25$ and $\text{BRE}_t \ge 0.65$ when verified volume $\text{RVOL} \ge 1.20$ is present).
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Confirmed bullish displacement ($\text{Close} > \text{Open}$, $\text{DR} \ge \theta_{\text{DR}}$, $\text{BRE} \ge \theta_{\text{BRE}}$) with $\text{RVOL} \ge \theta_{\text{RVOL}}$ (or passing strict price-only threshold $\text{DR} \ge 1.50, \text{BRE} \ge 0.75$ when `require_volume_data == FALSE`).
  - `SELL`: Confirmed bearish displacement ($\text{Close} < \text{Open}$, $\text{DR} \ge \theta_{\text{DR}}$, $\text{BRE} \ge \theta_{\text{BRE}}$) with $\text{RVOL} \ge \theta_{\text{RVOL}}$ (or passing strict price-only threshold when `require_volume_data == FALSE`).
  - `NEUTRAL`: Low-displacement indecisive candles (dojis, overlapping small bodies) or declining volume ($\text{RVOL} < 0.85$) on directional attempts.
- **Explanation:** E.g., `"Institutional Bullish Displacement confirmed: DR 1.62x ATR, BRE 81%, RVOL 1.85x 20-bar SMA (Confidence: 84.5%)."`
- **Timestamp:** Confirmed candle close UTC.
- **Dependencies:** Confirmed OHLCV Ingestion Service.
- **Unit Tests:** Test (1) full OHLCV with high RVOL, (2) missing volume on `BTCUSD` or `require_volume_data=TRUE` (must output `ABSTAIN_DATA_UNAVAILABLE`), and (3) missing volume with `require_volume_data=FALSE` (verify $C_{\text{missing\_volume}} \le 70.00$ and strictly `< C_{\text{with\_volume}}$ for identical OHLC).
- **Limitations:** In spot FX/Gold (`XAUUSD`), volume is decentralized tick volume from the liquidity provider rather than centralized exchange volume.

---

#### Brain 11: Volatility and Session (`BRAIN_11_VOLATILITY_SESSION`)
- **Purpose:** Evaluate whether current market volatility regime and active trading session timing provide favorable liquidity conditions for a trade in the specific direction.
- **Responsibilities:** Filter out dead/illiquid rollover hours, low-volatility compression traps, and extreme erratic volatility spikes using a mathematically contiguous `[0.00, 100.00]` ATR percentile partition and DST-aware `America/New_York` / `Europe/London` session clocks.
- **Required Inputs:** Confirmed OHLCV series (minimum 114 confirmed bars for 14-period ATR + 100-bar rolling percentile rank; 36 bars on `1MO`), UTC timestamp, IANA timezone databases (`America/New_York`, `Europe/London`), market symbol (`XAUUSD` vs. `BTCUSD`), and Session High/Low levels.
- **Contiguous, Gap-Free, Overlap-Free ATR Percentile Regime Partition (`[0.00, 100.00]`):**
  Let $P = \text{ATR\_PR} \in [0.00, 100.00]$ denote the rolling 100-bar percentile rank of `ATR(14)`. Every possible value of $P \in [0.00, 100.00]$ maps to **one and only one** regime with explicit inclusive/exclusive interval boundaries:

| Volatility Regime Code | Exact Mathematical Interval | Boundary Inclusion Rule | Brain 11 Directional Eligibility & Confidence Multiplier |
| :--- | :--- | :--- | :--- |
| **1. `DEAD_COMPRESSED`** | $0.00 \le P < 10.00$ | Includes `0.00`, excludes `10.00` | **Non-Tradable Dead Market:** Forces Brain 11 `vote = 'NEUTRAL'`, `confidence = 0.00`. |
| **2. `LOW_TRANSITIONAL`** | $10.00 \le P < 15.00$ | Includes `10.00`, excludes `15.00` | **Early Expansion Caution:** Allows directional vote (`BUY`/`SELL`) **only** for Sniper POI reversals during Killzones; applies `0.60x` volatility confidence weight (Fast Scalper blocked $\rightarrow$ `NEUTRAL`). |
| **3. `OPTIMAL_EXPANSION`** | $15.00 \le P \le 88.00$ | Includes both `15.00` and `88.00` | **Optimal Institutional Regime:** Full directional eligibility for both Sniper and Fast Scalper setups (`1.00x` volatility confidence weight; peaks at $P \in [50.00, 75.00]$). |
| **4. `ELEVATED_CAUTION`** | $88.00 < P \le 95.00$ | Excludes `88.00`, includes `95.00` | **High-Volatility Caution:** Allows directional vote only when displacement and session confluence are aligned; applies `0.50x` volatility confidence weight and signals wider ATR stop buffer. |
| **5. `EXTREME_SHOCK`** | $95.00 < P \le 100.00$ | Excludes `95.00`, includes `100.00` | **Erratic Volatility Shock Veto:** Forces Brain 11 `vote = 'NEUTRAL'`, `confidence = 0.00` (and triggers Phase 6 Volatility Shock protection if $P > 97.00$ or single bar $> 3.5 \times \text{ATR}$). |

- **DST-Aware Session Context (`XAUUSD` via `America/New_York` & `Europe/London`):**
  - **Rollover Dead Zone (`16:45–18:15 America/New_York`):** Encompasses the daily `17:00–18:00 America/New_York` CME/Bullion close and 15-minute pre/post spread-widening buffer (`20:45–22:15 UTC` in `EDT`; `21:45–23:15 UTC` in `EST`). Non-tradable on intraday timeframes (`1M`–`1H`).
  - **Asian Session (`18:00–03:00 America/New_York`):** Range formation / accumulation.
  - **London Open / Killzone (`08:00–11:30 Europe/London`) & NY Open / Overlap (`08:00–12:30 America/New_York`):** Peak institutional liquidity displacement windows.
- **Session Context (`BTCUSD`):** 24/7 operation with liquidity weighting across Asian (`00:00–08:00 UTC`), European (`08:00–16:30 Europe/London`), and US Equity Hours (`09:30–16:00 America/New_York`), plus weekend liquidity threshold adjustment.
- **Analysis Methodology:** On intraday timeframes (`1M` through `1H`), evaluates whether the current timestamp sits in an active liquidity window with `OPTIMAL_EXPANSION` (or qualifying `LOW_TRANSITIONAL` / `ELEVATED_CAUTION`) volatility and directional session expansion. On higher timeframes (`4H`, `1D`, `1W`, `1MO`), intraday hour-of-day filter is bypassed in favor of the 5-tier ATR percentile regime and multi-bar true-range expansion analysis.
- **Validation Rules:** UTC clock synchronization required (`NTP` drift check) + valid IANA timezone conversion.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Active tradable session + eligible volatility regime ($10.00 \le P \le 95.00$ per rules above) + price expanding bullishly above session equilibrium / post-session low sweep.
  - `SELL`: Active tradable session + eligible volatility regime ($10.00 \le P \le 95.00$ per rules above) + price expanding bearishly below session equilibrium / post-session high sweep.
  - `NEUTRAL`: Rollover dead window (`16:45–18:15 America/New_York`), `DEAD_COMPRESSED` ($P < 10.00$), `EXTREME_SHOCK` ($P > 95.00$), or mid-session equilibrium chop.
- **Confidence Calculation:** Session liquidity quality weight (40%), ATR percentile optimality curve across $[10.00, 95.00]$ (40%), and session range expansion alignment (20%).
- **Explanation:** E.g., `"NY/London Overlap Active (09:30 America/New_York / 13:30 UTC EDT): Volatility in OPTIMAL_EXPANSION regime (ATR_PR: 68.4%), bullish expansion above London equilibrium."`
- **Timestamp:** Confirmed candle close UTC + local `America/New_York` session timestamp.
- **Error Handling & Missing-Data Behaviour:** If `< 114` confirmed bars exist on `1M`–`1W` (or `< 36` bars on `1MO`) to compute the ATR percentile rank, or if timestamp timezone is unverified, returns `ABSTAIN_DATA_UNAVAILABLE` (`ERR_BRAIN11_INSUFFICIENT_ATR_HISTORY`).
- **Dependencies:** Market Session Clock & Volatility Service.
- **Unit Tests:** Test exact boundary values $P \in \{0.0, 9.99, 10.0, 14.99, 15.0, 88.0, 88.01, 95.0, 95.01, 100.0\}$, test `XAUUSD` rollover window in both EDT (`21:30 UTC`) and EST (`22:30 UTC`), and test `< 114` bar abstention.
- **Limitations:** Holiday schedules (e.g., US Bank Holidays) reduce NY session liquidity and are enforced in coordination with Phase 6 Market Calendar protection.

---

#### Brain 12: Precision Entry (`BRAIN_12_PRECISION_ENTRY`)
- **Purpose:** Validate the exact tactical execution trigger candle, Premium/Discount dealing-range location, and immediate structural Risk-to-Reward (`R:R`) feasibility before casting the final execution vote.
- **Responsibilities:** Act as the tactical gatekeeper ensuring we never buy at the top of a Premium dealing range (in Sniper mode) or enter a setup where the nearest structural Stop Loss produces an unacceptable `R:R` ratio.
- **Required Inputs:** Confirmed OHLCV series, active Dealing Range `[Swing_Low, Swing_High]`, active POI (`OB`/`BB`/`MB`/`FVG`/`Sweep` zone), candidate Stop Loss and Take Profit levels (computed via Section 15.1 Sniper & Fast Scalper formulas), and trading style mode (`SNIPER` vs. `FAST_SCALPER`).
- **Indicators & Calculations:**
  - **Dealing Range Position (`DRP`):** $\text{DRP} = \frac{\text{Close}_t - \text{Range\_Low}}{\text{Range\_High} - \text{Range\_Low}} \in [0.0, 1.0]$.
    - `DISCOUNT`: $\text{DRP} < 0.50$ (Optimal for Sniper `BUY`; Deep Discount / OTE Zone: $0.214 \le \text{DRP} \le 0.382$).
    - `EQUILIBRIUM`: $\text{DRP} = 0.50$.
    - `PREMIUM`: $\text{DRP} > 0.50$ (Optimal for Sniper `SELL`; Deep Premium / OTE Zone: $0.618 \le \text{DRP} \le 0.786$).
  - **Trigger Candle Anatomy:** Confirmation close rejecting POI (e.g., bullish rejection pinbar, bullish engulfing, or displacement close out of entry zone).
  - **Instantaneous Structural `R:R` Check:** $\text{RR}_1 = \frac{|\text{TP}_1 - \text{Entry}|}{|\text{Entry - SL}|}$ and $\text{RR}_2 = \frac{|\text{TP}_2 - \text{Entry}|}{|\text{Entry - SL}|}$.
- **Analysis Methodology:**
  - For **Sniper Entry:** Requires price to be in `DISCOUNT` (for `BUY`) or `PREMIUM` (for `SELL`), interacting with an institutional POI, printing a confirmed rejection/displacement trigger candle, and achieving $\text{RR}_2 \ge \theta_{\text{min\_rr\_sniper}}$ (default `2.0R`).
  - For **Fast Scalper Entry:** Allows continuation entries past Equilibrium provided a fresh breakaway FVG/BOS displacement occurred, stop distance is bounded by the deterministic Fast Scalper Micro-Impulse Anchor (Section 15.1), and net $\text{RR}_1 \ge \theta_{\text{min\_rr1\_scalp}}$ (default `1.2R`) and $\text{RR}_2 \ge \theta_{\text{min\_rr2\_scalp}}$ (default `1.8R`) before the next opposing liquidity obstacle.
- **Validation Rules:** `Entry != SL`, `Range_High > Range_Low`.
- **BUY / SELL / NEUTRAL Output:**
  - `BUY`: Confirmed bullish trigger candle at valid Long Entry Zone + valid Discount/Continuation location + structural `R:R` passes minimum threshold.
  - `SELL`: Confirmed bearish trigger candle at valid Short Entry Zone + valid Premium/Continuation location + structural `R:R` passes minimum threshold.
  - `NEUTRAL`: Price overextended away from entry zone (chasing), poor `R:R` due to wide SL or nearby opposing resistance/support, or no confirmed trigger candle close.
- **Confidence Calculation:** Dealing range location / OTE precision (35%), trigger candle close quality (35%), and clear structural R:R headroom (30%).
- **Explanation:** E.g., `"Sniper Long Entry Trigger confirmed: Price in Discount (31.2% of Dealing Range), bullish engulfing close off POI, structural R:R to TP2 is 1:3.4."`
- **Timestamp:** Confirmed candle close UTC.
- **Error Handling & Missing-Data Behaviour:** Returns `ABSTAIN_DATA_UNAVAILABLE` if dealing range or SL/TP boundaries cannot be calculated.
- **Dependencies:** Phase 2 Dealing Range (`ISMCStateProvider`) & Phase 5 Risk/Entry Calculator.
- **Unit Tests:** Test Sniper Buy in Premium (must reject / output `NEUTRAL`), Sniper Buy in Discount OTE with valid trigger and R:R (outputs `BUY`), Fast Scalper continuation with Micro-Impulse SL, and overextended candle with poor R:R (outputs `NEUTRAL`).
- **Limitations:** Dependent on accurate Dealing Range anchor selection from Phase 2.

---

## 12. Institutional & Smart Money Concepts (SMC) Architecture

Phase 2 formalizes **26 institutional and Smart Money Concepts (SMC)** features. Every concept is computed algorithmically from verified OHLCV data without claiming access to non-public commercial bank order books.

### 12.1 Complete SMC Feature Specification Matrix

| # | SMC Feature | Meaning | Detection Method | Confirmation Rule | Invalidation Rule | Timeframe & Data Requirements | Testing Requirements |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | **BOS (Break of Structure)** | Trend-continuation structural break in the direction of the existing trend. | Price breaks above prior confirmed Swing High in an uptrend (or below prior Swing Low in a downtrend). | Confirmed candle **body close** beyond the swing level + minimum ATR displacement check. | Wick-only pierce without body close is classified as a sweep, not BOS. | All 9 timeframes (`1M`–`1MO`); confirmed OHLC series. | Unit test verifying body close vs. wick rejection on synthetic HH/HL and LH/LL series. |
| **2** | **CHoCH (Change of Character)** | First early structural sign of potential trend reversal (breaking the most recent internal swing pivot against the prevailing trend). | In an uptrend, price breaks below the last internal Higher Low; in a downtrend, price breaks above the last internal Lower High. | Confirmed candle **body close** beyond the internal swing pivot. | Reclaimed by continuation BOS in the original trend direction before external structure breaks. | All 9 timeframes; uses `internal_pivot_len` lookback. | Test internal pivot break following a liquidity sweep vs. minor noise inside a large candle. |
| **3** | **MSS (Market Structure Shift)** | High-conviction structural trend reversal backed by a liquidity sweep and strong displacement. | Price sweeps an HTF/external liquidity pool (`BSL`/`SSL`) and breaks the structural swing pivot with an aggressive displacement impulse creating an FVG. | Confirmed candle body close beyond structural pivot + FVG creation + displacement ratio $\ge \theta_{\text{DR}}$. | Confirmed close back beyond the sweep extreme that initiated the MSS. | All 9 timeframes; OHLC + ATR(14). | Test MSS requiring all 3 criteria: (1) sweep, (2) structural break close, (3) FVG displacement. |
| **4** | **Internal & External Structure** | Dual-horizon structural hierarchy: External defines the primary dealing range; Internal defines pullbacks and tactical continuation/CHoCH inside that range. | Dual fractal detectors operating simultaneously with `L_int < L_ext` (e.g., Internal pivot length 3 vs. External pivot length 10). | Confirmed after `L_int` and `L_ext` right-hand candle closes respectively. | External structure updates only when external swing high/low is broken by body close. | All 9 timeframes; minimum 200 bars history (`>= 60` on `1MO`). | Test nesting of multiple internal swings inside a single external dealing range leg. |
| **5** | **Swing Highs & Swing Lows** | Confirmed local price maxima (`SH`) and minima (`SL`) anchoring market structure and liquidity pools. | $H_i > \max(H_{i-k \dots i-1})$ and $H_i \ge \max(H_{i+1 \dots i+k})$ for Swing High (analogous for Swing Low). | Strictly confirmed only after $k$ subsequent candles have closed (`t >= i + k`). | Never retroactively deleted; marked `BROKEN` or `SWEPT` when violated by future price action. | All 9 timeframes; zero future lookahead (`t >= i + k` enforced). | Repainting test verifying pivot $i$ never appears at bar $i$ or $i+1$, only at bar $i+k$. |
| **6** | **Buy-Side Liquidity (`BSL`)** | Resting buy-stop orders (short sellers' protective stops and breakout buyers' pending orders) positioned above Swing Highs, EQH, PDH, PWH, or Session Highs. | Any confirmed, untouched Swing High, EQH cluster, Session High, PDH, or PWH above current price (`State: ACTIVE_UNMITIGATED`). | Confirmed once the underlying swing pivot or session/day boundary closes. | Transitions `ACTIVE_UNMITIGATED` $\rightarrow$ `RAIDED_UNDER_EVALUATION` on `High > BSL_Level`, then to `SWEPT_RECLAIMED` or `INVALIDATED_BROKEN_BOS`. | All 9 timeframes; OHLC + IANA timezone clocks. | Test BSL registration and 7-state lifecycle transition upon `High > BSL`. |
| **7** | **Sell-Side Liquidity (`SSL`)** | Resting sell-stop orders (long traders' protective stops and breakdown sellers' pending orders) positioned below Swing Lows, EQL, PDL, PWL, or Session Lows. | Any confirmed, untouched Swing Low, EQL cluster, Session Low, PDL, or PWL below current price (`State: ACTIVE_UNMITIGATED`). | Confirmed once the underlying swing pivot or session/day boundary closes. | Transitions `ACTIVE_UNMITIGATED` $\rightarrow$ `RAIDED_UNDER_EVALUATION` on `Low < SSL_Level`, then to `SWEPT_RECLAIMED` or `INVALIDATED_BROKEN_BOS`. | All 9 timeframes; OHLC + IANA timezone clocks. | Test SSL registration and 7-state lifecycle transition upon `Low < SSL`. |
| **8** | **Equal Highs (`EQH`) & Equal Lows (`EQL`)** | Two or more swing highs or swing lows terminating at approximately the same price level, creating an engineered magnet of concentrated stop liquidity. | Two or more untouched confirmed Swing Highs (or Lows) where $\|P_1 - P_2\| \le \tau_{\text{eq}} \cdot \text{ATR}(14)$ without any intermediate bar violating the outer extreme. | Confirmed when the second (or $n$-th) swing pivot completes its $k$-bar confirmation. | Enters `RAIDED_UNDER_EVALUATION` when price trades above $\max(P_{\text{EQH}})$ or below $\min(P_{\text{EQL}})$. | All 9 timeframes; timeframe-specific $\tau_{\text{eq}}$ tolerance. | Test 2-touch and 3-touch EQH/EQL clusters within ATR tolerance and rejection of levels separated by an intermediate sweep. |
| **9** | **Liquidity Sweeps** | Intentional raid of a `BSL` or `SSL` pool to trigger resting stops and fill institutional counter-orders, followed by price rejection back inside the range. | Pool transitions from `ACTIVE_UNMITIGATED` $\rightarrow$ `RAIDED_UNDER_EVALUATION` $\rightarrow$ `SWEPT_RECLAIMED` within 1–2 confirmed bars (`High > BSL & Close < BSL` or `Low < SSL & Close > SSL`). | Confirmed candle close back inside the swept level with wick rejection ratio $\ge \theta_{\text{wick}}$. | Subsequent candle closes beyond the sweep extreme (`INVALIDATED_BROKEN_BOS`) or `sweep_expiry_bars` elapses (`CONSUMED_ARCHIVED`). | All 9 timeframes; Unified Liquidity Pool Registry. | Test 1-bar sweep, 2-bar sweep reclaim, and breakout invalidation. |
| **10** | **Stop-Hunt Proxies** | Algorithmic proxy detecting rapid wick expansion into a known liquidity pool accompanied by elevated tick/exchange volume and immediate intrabar mean reversion. | Combination of Liquidity Sweep (`SWEPT_RECLAIMED`) + wick length $\ge 1.2 \times \text{ATR}(14)$ + $\text{RVOL} \ge 1.3$ + close in opposite third of candle range. | Confirmed on candle close meeting all four proxy criteria. | Confirmed close beyond the stop-hunt wick extreme. | All 9 timeframes; OHLCV data (explicitly labeled as an OHLCV/Volume proxy, not bank level-3 data). | Test synthetic stop-hunt spike vs. normal low-volume wick. |
| **11** | **Liquidity Pools** | Aggregated price zones containing overlapping liquidity sources (e.g., `PDH` + `London High` + `15M EQH` within a tight ATR band). | Spatial interval clustering of all `ACTIVE_UNMITIGATED` `BSL` or `SSL` levels within $\Delta P \le 0.5 \cdot \text{ATR}(14)$, weighted by source hierarchy. | Confirmed when $\ge 2$ distinct liquidity objects cluster in the same price band. | Transitions through `RAIDED_UNDER_EVALUATION` $\rightarrow$ `SWEPT_RECLAIMED` / `CONSUMED_ARCHIVED` once outer bound is raided. | All 9 timeframes; multi-source liquidity registry. | Test overlapping PDH + EQH score boost vs. isolated minor swing high. |
| **12** | **Order Blocks (`OB`)** | Institutional footprint zone: the final opposing candle(s) prior to an impulsive displacement move that breaks structure and creates an FVG. | Last bearish candle before bullish displacement + BOS + FVG (Bullish OB); last bullish candle before bearish displacement + BOS + FVG (Bearish OB). | Confirmed only after the subsequent impulse completes a confirmed `BOS`/`MSS` and leaves an `FVG`. | **Mitigation:** Touch of `[MT, Proximal]` (`MITIGATED_SHALLOW_ACTIVE`) or `(Distal, MT)` (`MITIGATED_DEEP_ACTIVE`, -30pt confidence penalty). **Hard Invalidation:** Confirmed candle **body close** beyond `Distal Edge` (`INVALIDATED`). | All 9 timeframes; OHLCV + Structure + FVG modules. | Test 6-state OB lifecycle: creation, shallow touch holding 50% MT, deep touch holding Distal, consumed after expansion, and distal close invalidation. |
| **13** | **Breaker Blocks (`BB`)** | A failed Order Block that formed after a liquidity sweep and was impulsively broken through by an opposing `MSS` with displacement, flipping its polarity. | When an OB preceded by a liquidity sweep transitions to `INVALIDATED` via an opposing `MSS` with displacement (`DR >= 1.25`), re-classify the broken OB bounds as an active Breaker Block (`CONVERTED_TO_BREAKER_BLOCK`). | Confirmed on the `MSS` displacement candle body close through the old OB's `Distal Edge`. | Confirmed candle body close back through the distal side of the Breaker Block. | All 9 timeframes; requires OB + Liquidity Sweep + MSS modules. | Test Bullish OB failure (after sweep) converting into Bearish Breaker Block and subsequent bearish retest. |
| **14** | **Mitigation Blocks (`MB`)** | A structural failure swing zone (where a prior OB failed via an `MSS` after a failure swing that did **not** sweep the prior swing high/low). | When an OB formed without a preceding liquidity sweep transitions to `INVALIDATED` via an opposing `MSS`, re-classify the broken OB bounds as a Mitigation Block. | Confirmed on the candle body close breaking the failure swing OB's `Distal Edge`. | Confirmed candle body close back through the distal boundary of the Mitigation Block. | All 9 timeframes; OHLC + Structure + OB modules. | Differentiate Breaker Block (preceded by sweep) vs. Mitigation Block (preceded by failure swing without sweep). |
| **15** | **Fair Value Gaps (`FVG`)** | 3-candle price delivery inefficiency where buying or selling pressure was so one-sided that candle 1's range and candle 3's range do not overlap. | Bullish (`BISI`): $\text{Low}_t > \text{High}_{t-2}$. Bearish (`SIBI`): $\text{High}_t < \text{Low}_{t-2}$, filtered by minimum ATR gap height. | Confirmed on the close of candle $t$ (the 3rd candle of the pattern). | Invalidated when a confirmed candle closes completely beyond the distal boundary of the gap. | All 9 timeframes; contiguous 3-candle OHLC sequence. | Test BISI, SIBI, 50% Consequent Encroachment (`CE`), and gap-size ATR filter. |
| **16** | **Inverse Fair Value Gaps (`IFVG`)** | A previously valid FVG that was impulsively disrespected by an opposing candle body close, inverting the gap into an opposing support/resistance zone. | Track an existing Bullish or Bearish FVG; when an opposing candle closes completely through the distal edge of the gap, register an IFVG of opposite polarity with the same price bounds. | Confirmed on the close of the candle that breaks through the original FVG's distal edge. | Confirmed candle body close back through the opposite side of the IFVG. | All 9 timeframes; depends on FVG lifecycle registry. | Test Bearish FVG broken upward converting to Bullish IFVG and acting as support on pullback. |
| **17** | **Displacement** | High-velocity, large-bodied institutional price expansion indicating aggressive market-order execution. | Candle body size $\ge \theta_{\text{DR}} \cdot \text{ATR}(14)$ and body-to-range efficiency $\ge 0.65$, optionally spanning a 1-to-3 bar contiguous directional leg that creates an FVG. | Confirmed on candle close meeting displacement thresholds. | Loss of displacement when subsequent counter-candle immediately retraces $> 100\%$ of the impulse candle. | All 9 timeframes; OHLC + ATR(14). | Test single-bar and 2-bar displacement legs vs. long-wick indecisive high-range candles. |
| **18** | **Imbalances (Volume / Wick / Opening Gaps)** | Price inefficiencies beyond standard 3-candle FVGs, including Volume Imbalances (body-to-body gap with overlapping wicks) and Opening Liquidity Voids. | Volume Imbalance: $\text{Open}_t > \text{Close}_{t-1}$ (bullish) or $\text{Open}_t < \text{Close}_{t-1}$ (bearish) where wicks overlap; Opening Gap: $\text{Low}_t > \text{High}_{t-1}$ or $\text{High}_t < \text{Low}_{t-1}$. | Confirmed on candle close of bar $t$. | Filled and closed through by subsequent confirmed candle body. | All 9 timeframes (especially `XAUUSD` session/weekend opens and high-velocity `1M`–`15M` bars). | Test body-to-body Volume Imbalance detection and fill tracking. |
| **19** | **Premium & Discount** | Valuation zones within the active Dealing Range: upper 50% (`0.50 to 1.00`) is **Premium** (expensive — favorable for shorts); lower 50% (`0.00 to 0.50`) is **Discount** (cheap — favorable for longs). | Compute normalized position $\text{DRP} = (\text{Price} - \text{DL}_{\text{low}}) / (\text{DL}_{\text{high}} - \text{DL}_{\text{low}})$ along with Optimal Trade Entry (`OTE`: `0.618–0.786` retracement). | Confirmed as soon as the anchoring Dealing Range (`DL_low`, `DL_high`) is confirmed. | Recalculated dynamically when a new external `BOS` or `MSS` establishes a new Dealing Range. | All 9 timeframes; depends on Dealing Range module. | Test DRP math: `0.25` = Discount, `0.50` = Equilibrium, `0.75` = Premium. |
| **20** | **Equilibrium (`EQ`)** | The exact 50% midpoint ($0.50$) of an active Dealing Range, Order Block (Mean Threshold), or Fair Value Gap (Consequent Encroachment). | $\text{EQ} = \frac{\text{Upper\_Bound} + \text{Lower\_Bound}}{2}$. | Confirmed simultaneously with the parent Dealing Range, OB, or FVG. | Updates or retires whenever the parent range/zone is updated or invalidated. | All 9 timeframes. | Verify exact midpoint calculation and classification boundary at `0.50`. |
| **21** | **Dealing Range** | The active structural trading boundary anchored by a confirmed External Swing Low and External Swing High after a liquidity sweep and/or structural break (`BOS`/`MSS`). | Anchored from the origin swing pivot that initiated the `BOS` to the newly confirmed external swing extreme once a pullback begins. | Confirmed once the terminating swing extreme completes its $k$-bar pivot confirmation. | Replaced only when a confirmed candle body closes outside `[Dealing_Low, Dealing_High]`. | All 9 timeframes; External Structure module. | Test dealing range persistence during internal pullbacks and update upon external BOS. |
| **22** | **Inducement (`IDM`)** | Minor internal structural pullback pivot or liquidity pool engineered near an institutional POI to entice early entries before the true sweep into the POI occurs. | First internal swing pullback low (in a bullish leg after BOS) or internal swing pullback high (in a bearish leg after BOS) located above/below the unmitigated origin OB/FVG. | Confirmed when the internal pivot forms between current price and the origin OB/FVG. | Marked `SWEPT/COMPLETE` once price raids the IDM level, unlocking high-probability entry at the underlying OB/FVG. | All 9 timeframes; Internal Structure + OB/FVG modules. | Verify that an OB entry receives higher SMC quality score after internal IDM has been swept vs. before IDM is swept. |
| **23** | **Supply and Demand Zones** | Broader accumulation/distribution base zones (Rally-Base-Drop / Drop-Base-Rally) preceding an impulsive imbalance departure. | Identify 1-to-5 candle consolidation base ($\text{Range} < 0.8 \cdot \text{ATR}$) followed by an impulsive departure leg $> 2.0 \cdot \text{ATR}$ breaking structure. | Confirmed on the close of the departure impulse leg. | Confirmed candle body close beyond the distal edge of the base zone. | All 9 timeframes; complements single-candle OB analysis. | Test Drop-Base-Rally (Demand) and Rally-Base-Drop (Supply) detection and distal invalidation. |
| **24** | **Session Liquidity** | High and Low price extremes formed during distinct global institutional trading sessions (Asian, London, New York). | Track running High and Low between IANA timezone-aware session boundaries (`America/New_York` for Asian `18:00–03:00` and NY `08:00–17:00`; `Europe/London` for London `08:00–16:30`). | Session High/Low locks as a static liquidity pool (`ACTIVE_UNMITIGATED`) once the session end timestamp closes. | Transitions through the 7-state liquidity lifecycle when a subsequent session breaches the prior Session High/Low. | Intraday timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`); IANA DST-aware session clock. | Test Asian High/Low locking and London Open sweep of Asian High/Low across both EST and EDT dates. |
| **25** | **Previous Day High / Low (`PDH` / `PDL`)** | The exact highest high (`PDH`) and lowest low (`PDL`) of the most recently completed `1D` daily trading session—major daily institutional liquidity benchmarks. | Extracted from the last confirmed `1D` candle (using `17:00 America/New_York` rollover for `XAUUSD`—`21:00 UTC` EDT / `22:00 UTC` EST—and `00:00 UTC` for `BTCUSD`). | Confirmed immediately upon the daily session close timestamp. | Transitions through the 7-state liquidity lifecycle upon breach during the current day; rolls over at the next daily close. | All intraday and daily timeframes (`1M` through `1D`). | Test PDH/PDL computation across weekend rollover and EST/EDT transitions for `XAUUSD`. |
| **26** | **Previous Week High / Low (`PWH` / `PWL`)** | The exact highest high (`PWH`) and lowest low (`PWL`) of the most recently completed `1W` weekly candle—major macro liquidity benchmarks. | Extracted from the last confirmed `1W` candle. | Confirmed upon the weekly close boundary. | Transitions through the 7-state liquidity lifecycle upon breach during the current week; updates at the start of each new trading week. | All timeframes (`1M` through `1W`). | Test PWH/PWL locking at weekly close and persistence across all intraday bars of the following week. |

---

## 13. Multi-Timeframe (MTF) Intelligence Architecture

Phase 3 governs how all **nine timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`)** synchronize and cross-validate without lookahead bias or repainting.

### 13.1 Core MTF Architectural Components

1. **Higher Timeframe Bias (`HTF_BIAS`):**
   - Evaluates the mapped `HTF 1` and `HTF 2` (from the non-duplicating table in Section 9.2) to classify the macro environment as `BULLISH_EXPANSION`, `BULLISH_PULLBACK`, `BEARISH_EXPANSION`, `BEARISH_PULLBACK`, `NEUTRAL_CONFLICT`, or `TOP_OF_HIERARCHY_NO_HTF` (for `1MO`).
2. **Lower Timeframe Confirmation (`LTF_CONFIRM`):**
   - When an execution timeframe (`T_exec`, e.g., `1H`) taps an institutional POI, the optional `LTF` (e.g., `15M`, or `1W` when `T_exec == 1MO`) can be inspected for an internal `CHoCH`/`MSS` + displacement close occurring inside the `T_exec` POI before the `T_exec` candle closes, **provided and only provided** that final `T_exec` signal emission respects the user's selected confirmation mode (`T_exec` confirmed candle close).
3. **Six-Dimensional MTF Alignment Matrix:**
   Every Mode B evaluation computes an explicit alignment state (`ALIGNED_BULLISH`, `ALIGNED_BEARISH`, `NEUTRAL`, `CONFLICT`, or `NOT_APPLICABLE_TOP_TF`) across six dimensions:
   - **Trend Alignment:** Concordance of Brain 1 across `T_exec`, `HTF 1`, and `HTF 2` (or `T_exec` and `HTF 1 = 1MO` when `T_exec == 1W`).
   - **Structure Alignment:** External `BOS`/`MSS` concordance across `T_exec` and `HTF 1` (or `T_exec` internal structure aligning with `HTF 1` external continuation after a discount/premium pullback).
   - **Liquidity Alignment:** Verifies that `T_exec`'s target (`TP1`/`TP2`) flows in the direction of `HTF 1`'s active Draw on Liquidity (`BSL`/`SSL`).
   - **SMC Alignment:** Ensures `T_exec` is not firing a `BUY` signal directly beneath an active `HTF 1` Bearish Order Block/FVG (or a `SELL` signal directly into an active `HTF 1` Bullish Order Block/FVG).
   - **Momentum Alignment:** Checks that `HTF 1` momentum is not violently opposing `T_exec` entry direction.
   - **Volatility Alignment:** Verifies that neither `T_exec` nor `HTF 1` is locked in `DEAD_COMPRESSED` or `EXTREME_SHOCK` state.
4. **Conflicting Timeframe Detection & Veto Rules:**
   - **Hard Conflict (`MTF_VETO`):** If `T_exec` signals `BUY`, while `HTF 1` has just printed a confirmed Bearish `MSS`/Displacement or price is capped inside an active `HTF 1` Bearish OB, the MTF Engine triggers `MTF_CONFLICT_DETECTED = TRUE` and forces the Mode B Master Decision to `WAIT`.
   - **Counter-Trend Pullback Recognition (Allowed Only When Explicitly Configured):** Distinguishes between a blind conflict and a valid structural retrace (e.g., `HTF 1` is Bullish External Structure currently pulling back into a `HTF 1` Discount Bullish OB; `T_exec` flips from bearish pullback to Bullish `MSS` inside that `HTF 1` OB $\rightarrow$ classified as `ALIGNED_BULLISH_REENTRY`).

### 13.2 Non-Repainting, Timestamp Validation, and Lookahead-Bias Prevention

```
Timeline (UTC) for 15M Execution Timeframe with 1H HTF Confirmation:
13:00          13:15          13:30          13:45          14:00
  |---- 15M #1 --|---- 15M #2 --|---- 15M #3 --|---- 15M #4 --|
  |----------------------- 1H Candle (Forming) ---------------| (Closes at 14:00 UTC)
  ^
  Last Confirmed 1H Candle closed at 13:00 UTC (Covers 12:00 - 13:00 UTC)
```

- **Strict Cutoff Invariant:** When evaluating the `15M` candle closing at `13:15 UTC`, `13:30 UTC`, or `13:45 UTC`, the MTF Engine is **mathematically prohibited** from reading the `13:00–14:00 UTC` `1H` candle because that `1H` candle has not closed yet. It must strictly reference the `1H` candle that closed at `13:00 UTC`. Only when the `14:00 UTC` `15M` candle closes at `14:00 UTC` does the `13:00–14:00 UTC` `1H` candle become eligible for use.
- **Pine Script v6 Implementation Rule:** As fully specified in Section 19.1, every HTF query in Pine Script v6 must guarantee zero lookahead and zero historical-vs-realtime drift by evaluating `barstate.isconfirmed` inside the HTF context (`f_confirmed_htf_tuple()`) with `lookahead = barmerge.lookahead_off`.
- **Missing Data Handling in MTF:** If any required confirmation timeframe (`HTF 1` or `HTF 2`) has a missing candle or calendar-aware stale data status, Mode B outputs `WAIT` with status `MTF_DATA_STALE_OR_MISSING`.

---

## 14. Master Decision Engine

Phase 4 integrates the outputs of Phase 1 (12 Brains), Phase 2 (SMC), Phase 3 (MTF), Phase 5 (Risk Gate), and Phase 6 (News/Market Protection) into a single deterministic decision: **`BUY`**, **`SELL`**, or **`WAIT`**.

### 14.1 Decision Engine Pipeline & Strict Mode Logic

```
[Confirmed Candle Close on (Symbol, Execution_Timeframe)]
                        │
                        ▼
      ┌───────────────────────────────────┐
      │ Gate 1: Data & Feed Integrity     │──── Fail ───► WAIT (Reason: DATA UNAVAILABLE / STALE FEED)
      └─────────────────┬─────────────────┘
                        │ Pass
                        ▼
      ┌───────────────────────────────────┐
      │ Gate 2: Phase 6 Market & News     │──── Veto ───► WAIT (Reason: HIGH-IMPACT NEWS / NEWS FEED DISCONNECTED / SPREAD / VOL SHOCK)
      │         Protection Check          │
      └─────────────────┬─────────────────┘
                        │ Pass
                        ▼
      ┌───────────────────────────────────┐
      │ Gate 3: Phase 1 Twelve-Brain      │──── Data ───► If Mandatory Brain Abstains OR Active Quorum < Min ───► WAIT
      │         Equal Voting Evaluation   │     Check
      └─────────────────┬─────────────────┘
                        │
                        ▼
      ┌───────────────────────────────────┐
      │ Gate 4: Minimum Vote Threshold    │──── Fail ───► WAIT (Reason: INSUFFICIENT BRAIN CONSENSUS / BRAIN CONFLICT)
      │         & Conflict Check          │
      └─────────────────┬─────────────────┘
                        │ Pass
                        ▼
      ┌───────────────────────────────────┐
      │ Gate 5: Mandatory Core Brain,     │──── Fail ───► WAIT (Reason: SMC / MTF / PRECISION TRIGGER UNCONFIRMED)
      │         SMC & MTF Confirmation    │
      └─────────────────┬─────────────────┘
                        │ Pass
                        ▼
      ┌───────────────────────────────────┐
      │ Gate 6: Phase 5 Risk, R:R,        │──── Fail ───► WAIT (Reason: RISK LIMIT / INVALID R:R / DUPLICATE SIGNAL)
      │         & Duplicate Signal Gate   │
      └─────────────────┬─────────────────┘
                        │ Pass
                        ▼
           [EMIT CONFIRMED BUY OR SELL]
```

### 14.2 Equal Voting, Mode A / Mode B Tally Rules, and Strict Mode Consensus
1. **Equal Voting Tally Across All 12 Brains:**
   - $V_{\text{BUY}} = \sum_{i=1}^{12} \mathbb{I}(\text{Brain}_i.\text{vote} == \text{'BUY'})$
   - $V_{\text{SELL}} = \sum_{i=1}^{12} \mathbb{I}(\text{Brain}_i.\text{vote} == \text{'SELL'})$
   - $V_{\text{NEUTRAL}} = \sum_{i=1}^{12} \mathbb{I}(\text{Brain}_i.\text{vote} == \text{'NEUTRAL'})$
   - $V_{\text{ABSTAIN}} = \sum_{i=1}^{12} \mathbb{I}(\text{Brain}_i.\text{vote} == \text{'ABSTAIN\_DATA\_UNAVAILABLE'})$
   - Invariant: $V_{\text{BUY}} + V_{\text{SELL}} + V_{\text{NEUTRAL}} + V_{\text{ABSTAIN}} \equiv 12$.
2. **Exact Effect of Neutral Votes, Abstentions, Conflicts, and Mode A / `1MO` Boundaries:**
   - **`NEUTRAL` Votes:** A `NEUTRAL` vote means the brain had valid data, analyzed the market, and found no directional edge. It contributes `0` to $V_{\text{BUY}}$ and `0` to $V_{\text{SELL}}$, remaining in the denominator of active evaluated brains ($N_{\text{eligible}}$).
   - **`ABSTAIN_DATA_UNAVAILABLE` Votes (Gate 3 Data Quorum Rule):**
     - **Mandatory Brains (Zero Abstention Tolerance):** **Brain 1 (`Trend`)**, **Brain 3 (`Market Structure`)**, **Brain 7 (`Order Block`)**, **Brain 8 (`Fair Value Gap`)**, **Brain 11 (`Volatility/Session`)**, **Brain 12 (`Precision Entry`)**, and (in Mode B for `1M`–`1W`) **Brain 2 (`MTF`)** are **Mandatory Quorum Brains**. If any Mandatory Quorum Brain outputs `ABSTAIN_DATA_UNAVAILABLE`, Gate 3 immediately fails and outputs `WAIT` (`REASON: MANDATORY_BRAIN_DATA_UNAVAILABLE`).
     - **Non-Mandatory Brains (Maximum 1 Abstention Tolerance):** If more than `1` brain overall outputs `ABSTAIN_DATA_UNAVAILABLE` ($V_{\text{ABSTAIN}} > 1$), Gate 3 immediately fails and outputs `WAIT` (`REASON: INSUFFICIENT_BRAIN_DATA_QUORUM`).
   - **Eligible Active Brain Pool ($N_{\text{eligible}}$):**
     - In **Mode B (`MTF_CONFIRMED`) on `1M` through `1W`:** All 12 brains are active directional voters ($N_{\text{eligible}} = 12 - V_{\text{ABSTAIN}} \in \{11, 12\}$).
     - In **Mode A (`INDEPENDENT_TIMEFRAME`)** OR on **`1MO` (where no HTF exists above `1MO`):** Brain 2 is structurally non-directional (`INACTIVE_IN_MODE_A` / `TOP_OF_HIERARCHY_NO_HTF`, fixed at `NEUTRAL`), so the 11 single-timeframe brains (`Brain 1` and `Brains 3..12`) form the active directional pool ($N_{\text{eligible}} = 11 - V_{\text{ABSTAIN}} \in \{10, 11\}$).
3. **Minimum Voting Threshold (`STRICT` Mode — Proposed Baseline Subject to `PENDING FOUNDER DECISION`):**
   - **Mode B (`12` Active Brains):** Requires **$V_{\text{dir}} \ge 8$ out of $12$** directional votes (`BUY` or `SELL`) AND opposing votes **$V_{\text{opp}} \le 1$**.
   - **Mode A or `1MO` (`11` Active Single-Timeframe Brains):** Requires **$V_{\text{dir}} \ge 8$ out of $11$** directional votes (`BUY` or `SELL`) AND opposing votes **$V_{\text{opp}} \le 1$** (preserving the exact minimum 8-vote integer threshold, or configurable `7/11` proportional equivalent per Founder decision `PFD-03`).
   - **Brain Conflict Detection:** If opposing votes reach $V_{\text{opp}} \ge 2$ (e.g., $V_{\text{BUY}} = 8$ while $V_{\text{SELL}} = 2$), Gate 4 flags `BRAIN_CONFLICT_DETECTED` and defaults to `WAIT`.
4. **Mandatory Core Confirmation Requirements (Gate 5):**
   Even when the vote count passes Gate 4, `STRICT` mode requires all three core confirmations:
   - **Precision Entry Gate:** **Brain 12 (`Precision Entry`)** must vote in the signal direction (`BUY` for Long, `SELL` for Short).
   - **SMC Structural & POI Gate:** At least one structural brain (**Brain 3 `Market Structure`** or **Brain 5 `Liquidity Sweep`**) AND at least one POI brain (**Brain 7 `Order Block`** or **Brain 8 `Fair Value Gap`**) must vote in the signal direction, and neither pair may cast an opposing vote.
   - **MTF Gate (Mode B):** On `1M` through `1W`, **Brain 2 (`Multi-Timeframe Intelligence`)** must vote in the signal direction (`BUY` or `SELL`) and Phase 3 MTF alignment must report `has_conflict == FALSE`. On `1MO` in Mode B, Phase 3 verifies zero opposing `1W` LTF structural breakdown.
5. **Aggregate Confidence & Signal Quality Grade (`quality_grade`):**
   - **Aggregate Confidence ($C_{\text{agg}}$):** Average confidence of the brains voting in the winning direction, scaled by net consensus over the eligible active pool $N_{\text{eligible}}$:
     $$C_{\text{agg}} = \left(\frac{1}{V_{\text{dir}}} \sum_{i \in \text{dir}} C_i\right) \times \left(\frac{V_{\text{dir}} - V_{\text{opp}}}{N_{\text{eligible}}}\right) \in [0.00, 100.00]$$
     *(When `direction == 'WAIT'`, $C_{\text{agg}} = 0.00$.)*
   - **Signal Quality Tier (`quality_grade`):**
     - `A+` (Institutional Sniper Confluence): $V_{\text{dir}} \ge 10$ (or $\ge 9$ in 11-brain Mode A/`1MO`), $V_{\text{opp}} = 0$, $C_{\text{agg}} \ge 80.00\%$, MTF Aligned, SMC Sweep + OB/FVG confluence.
     - `A` (High Conviction): $V_{\text{dir}} \ge 9$, $V_{\text{opp}} \le 1$, $C_{\text{agg}} \ge 70.00\%$.
     - `B` (Standard Approved Strict Setup): Meets minimum `STRICT` vote threshold ($V_{\text{dir}} \ge 8$, $V_{\text{opp}} \le 1$) and passes all 6 mandatory gates.
     - `WAIT`: Any evaluation resolving to `direction == 'WAIT'`.
6. **Duplicate Signal Prevention & Invalidation (Gate 6):**
   - Once a confirmed `BUY` or `SELL` signal is emitted for a specific `(symbol, execution_timeframe, signal_type, poi_id / structural_leg_id)`, the engine suppresses duplicate identical signals on subsequent adjacent bars within the same Entry Zone while the existing signal remains `ACTIVE`.
   - A new same-direction signal on that timeframe can only fire after the previous signal reaches `TP1_HIT`/`INVALIDATED`/`EXPIRED` OR a fresh `BOS` forms a new distinct POI.

### 14.3 Mandatory Signal Output Schema (Complete 18-Field Contract)
Every emitted decision record (`BUY`, `SELL`, or `WAIT`) across the Database (`signals` + `trade_plans`), Backend REST/WebSocket API, TradingView Webhook, and Frontend UI must populate the following **exact 18 mandatory attributes**:

| # | Field Name | Data Type | Nullability | Validation Rules & Description |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `signal_id` | `UUIDv7` | `NOT NULL` | Time-ordered globally unique identifier for the signal evaluation record. |
| **2** | `symbol` | `ENUM('XAUUSD', 'BTCUSD')` | `NOT NULL` | Target canonical market instrument (`CHECK (symbol IN ('XAUUSD', 'BTCUSD'))`). |
| **3** | `direction` | `ENUM('BUY', 'SELL', 'WAIT')` | `NOT NULL` | Deterministic master decision output (`CHECK (direction IN ('BUY', 'SELL', 'WAIT'))`). |
| **4** | `execution_timeframe` | `ENUM('1M','5M','15M','30M','1H','4H','1D','1W','1MO')` | `NOT NULL` | Canonical internal QUANTUM timeframe that generated and owns this decision. |
| **5** | `signal_type` | `ENUM('INDEPENDENT_TIMEFRAME', 'MTF_CONFIRMED')` | `NOT NULL` | Mode A (`INDEPENDENT_TIMEFRAME`) vs. Mode B (`MTF_CONFIRMED`) identifier. |
| **6** | `timestamp` | `TIMESTAMPTZ` (ISO-8601 UTC) | `NOT NULL` | Confirmed execution candle close UTC timestamp (`candle_timestamp`). |
| **7** | `brain_votes` | `JSONB` | `NOT NULL` | Complete array of all 12 brain objects `{brain_number, brain_code, vote, confidence, explanation, evaluated_at}` + summary tally `{buy_count, sell_count, neutral_count, abstain_count, eligible_pool}`. Must contain exactly 12 brain entries. |
| **8** | `confidence` | `NUMERIC(5,2)` | `NOT NULL` | Aggregate confidence score $C_{\text{agg}} \in [0.00, 100.00]$ (`0.00` when `direction == 'WAIT'`). |
| **9** | `quality_grade` | `ENUM('A+', 'A', 'B', 'WAIT')` | `NOT NULL` | **Signal Quality Tier** as computed in Section 14.2 Rule 5 (`CHECK ((direction = 'WAIT' AND quality_grade = 'WAIT') OR (direction IN ('BUY','SELL') AND quality_grade IN ('A+','A','B')))`). |
| **10** | `mtf_status` | `JSONB` | `NOT NULL` | `{mode, htf1_tf, htf1_closed_ts, htf2_tf, htf2_closed_ts, ltf_tf, alignment_matrix, has_conflict, conflict_reason}`. |
| **11** | `smc_status` | `JSONB` | `NOT NULL` | `{external_structure, internal_structure, dealing_range_low, dealing_range_high, premium_discount_pct, active_poi, liquidity_draw, active_sweep}`. |
| **12** | `entry` | `JSONB` | `NULL` iff `WAIT` | `{entry_price, entry_zone_low, entry_zone_high, entry_style: 'SNIPER' \| 'FAST_SCALPER'}`. Required (`NOT NULL`) when `direction IN ('BUY', 'SELL')`; `NULL` when `direction == 'WAIT'`. |
| **13** | `sl` | `NUMERIC(18,6)` | `NULL` iff `WAIT` | Exact structural Stop Loss price (`CHECK (sl > 0 AND sl != entry_price)` when `direction IN ('BUY', 'SELL')`; `NULL` when `direction == 'WAIT'`). |
| **14** | `tp_levels` | `JSONB` | `NULL` iff `WAIT` | `{tp1_price, tp1_rr, tp2_price, tp2_rr, tp3_price, tp3_rr}`. Required (`NOT NULL`) when `direction IN ('BUY', 'SELL')`; `NULL` when `direction == 'WAIT'`. |
| **15** | `invalidation` | `JSONB` | `NOT NULL` | `{invalidation_price, invalidation_condition, expiry_timestamp, expiry_bars}` (for `WAIT`, specifies the structural price levels required to unlock a future setup). |
| **16** | `explanation` | `TEXT` | `NOT NULL` | Non-empty human-readable narrative explaining the exact reason for the `BUY`, `SELL`, or `WAIT` decision (`CHECK (length(trim(explanation)) > 0)`). |
| **17** | `strategy_version` | `VARCHAR(64)` | `NOT NULL` | Immutable semantic version tag of the active ruleset and parameter profile (e.g., `v1.1.0-strict`). |
| **18** | `signal_status` | `ENUM` | `NOT NULL` | `WAIT_NO_TRADE`, `ACTIVE`, `TP1_HIT`, `TP2_HIT`, `TP3_HIT`, `STOPPED_OUT`, `BREAKEVEN_CLOSED`, `INVALIDATED`, `EXPIRED`, `VETOED_BY_PROTECTION`. |

---

## 15. Entry, Execution, and Risk Management

Phase 5 translates an approved `BUY` or `SELL` signal into a precision trade plan and enforces portfolio-level risk constraints.

### 15.1 Entry, Stop Loss (Sniper & Fast Scalper), and Take Profit Engineering

| Component | Technical Calculation & Rules |
| :--- | :--- |
| **Entry Price & Entry Zone** | **Entry Price:** Confirmed close price of the trigger candle $C_t$. **Entry Zone:** Bounded interval `[entry_zone_low, entry_zone_high]` representing the proximal-to-50% Mean Threshold/Consequent Encroachment of the active Order Block, Breaker Block, or FVG. |
| **Sniper Entry & Sniper Stop Loss (`SL_sniper`)** | Triggered at Discount/Premium POI (`OB`, `BB`, `MB`, `FVG`, or `Sweep Reclaim`). Stop Loss is placed strictly beyond the POI's distal boundary and sweep wick extreme:<br>• **Sniper `BUY` (`SL`):** $\text{SL}_{\text{sniper\_buy}} = \min(\text{POI\_Distal\_Low}, \text{Sweep\_Wick\_Low}) - (\beta_{\text{sniper}} \cdot \text{ATR}(14) + \text{Current\_Spread})$<br>• **Sniper `SELL` (`SL`):** $\text{SL}_{\text{sniper\_sell}} = \max(\text{POI\_Distal\_High}, \text{Sweep\_Wick\_High}) + (\beta_{\text{sniper}} \cdot \text{ATR}(14) + \text{Current\_Spread})$<br>where $\beta_{\text{sniper}}$ is the timeframe-configured ATR buffer multiplier (default `0.15`). |
| **Fast Scalper Entry & Symmetrical Micro-Impulse Stop Loss (`SL_scalp`)** | Triggered on confirmed displacement breakout / micro-FVG continuation during active session liquidity. Uses a **3-Priority Deterministic Anchor Hierarchy** (strictly symmetrical for `BUY` and `SELL`):<br>**1. Primary Anchor (Breakaway Micro-FVG Origin Base):** When the trigger candle $C_t$ forms or retests a 3-candle breakaway Fair Value Gap $(C_{t-2}, C_{t-1}, C_t)$, the structural anchor is the base of the displacement middle candle $C_{t-1}$ and origin candle $C_{t-2}$:<br>• `BUY`: $A_{\text{primary\_buy}} = \min(\text{Low}_{t-1}, \text{Low}_{t-2})$<br>• `SELL`: $A_{\text{primary\_sell}} = \max(\text{High}_{t-1}, \text{High}_{t-2})$<br>**2. Fallback Anchor 1 (Micro-Impulse Pullback Pivot, when no 3-candle FVG exists):** Searches the contiguous micro-impulse leg window $[t-3, t]$ for the lowest confirmed candle low (for `BUY`) or highest confirmed candle high (for `SELL`) that initiated the `BOS` displacement:<br>• `BUY`: $A_{\text{fallback1\_buy}} = \min_{k \in \{0..2\}}(\text{Low}_{t-k})$<br>• `SELL`: $A_{\text{fallback1\_sell}} = \max_{k \in \{0..2\}}(\text{High}_{t-k})$<br>**3. Fallback Anchor 2 (Single-Bar Giant Marubozu Guard):** If the selected anchor distance $\|\text{Entry}_t - A\|$ exceeds `max_scalp_sl_atr * ATR(14)` (default `2.20 * ATR(14)`), the anchor tightens to the trigger displacement candle $C_t$'s own structural extreme ($\text{Low}_t$ for `BUY`, $\text{High}_t$ for `SELL`); if $\|\text{Entry}_t - \text{Extreme}_t\|$ still exceeds `2.50 * ATR(14)` or is smaller than `min_scalp_sl_atr * ATR(14)` (`0.35 * ATR(14)`), the Fast Scalper trade plan is **rejected and downgraded to `WAIT` (`REASON: SCALP_SL_OUT_OF_BOUNDS`)**.<br>**Final Symmetrical Fast Scalper Stop Loss Formula:**<br>• **Fast Scalper `BUY` (`SL`):** $\text{SL}_{\text{scalp\_buy}} = A_{\text{buy}} - (\beta_{\text{scalp}} \cdot \text{ATR}(14) + \text{Current\_Spread})$<br>• **Fast Scalper `SELL` (`SL`):** $\text{SL}_{\text{scalp\_sell}} = A_{\text{sell}} + (\beta_{\text{scalp}} \cdot \text{ATR}(14) + \text{Current\_Spread})$<br>where $\beta_{\text{scalp}}$ defaults to `0.10`. |
| **Take Profit 1 (`TP1`)** | Conservative first structural/liquidity hurdle (e.g., internal swing high/low, Dealing Range Equilibrium `50%`, or minimum `1.2R–1.5R`). Triggers Partial Profit scale-out and Break-Even rule. |
| **Take Profit 2 (`TP2`)** | Primary target aligned with external Dealing Range extreme or major `ACTIVE_UNMITIGATED` `BSL`/`SSL` pool (`EQH`/`EQL`, `PDH`/`PDL`, Session High/Low), typically `2.0R–3.5R`. |
| **Take Profit 3 (`TP3`)** | Runner target aligned with HTF Draw on Liquidity (`PWH`/`PWL`, HTF FVG/OB, or measured range extension), typically `3.5R–5.0R+`. |
| **Partial Profit & Break-Even (`BE`)** | Configurable rule per profile (e.g., at `TP1` hit: close `50%` of position and move `SL` to `Entry_Price + Commission/Spread_Offset`; at `TP2` hit: close `25%` and trail remaining `25%` behind confirmed internal swing pivots). |
| **Trailing Stop** | Structure-based trailing stop: trails behind newly confirmed internal Higher Lows (for `BUY`) or Lower Highs (for `SELL`) only after `TP1` is achieved. |
| **Risk-to-Reward (`R:R`) Gate** | Any candidate signal whose structural distance to the nearest opposing HTF barrier yields $\text{RR}(\text{TP}_1) < \theta_{\text{min\_rr1}}$ or $\text{RR}(\text{TP}_2) < \theta_{\text{min\_rr2}}$ is automatically rejected and downgraded to `WAIT`. |

### 15.2 Capital & Portfolio Risk Protection Rules

1. **Position Sizing & Risk Per Trade:**
   - Default risk per trade is configurable (e.g., `0.25%` to `1.00%` of account equity; hard cap enforced by risk profile).
   - Exact Position Size formula:
     $$\text{Position\_Units} = \frac{\text{Account\_Equity} \times \text{Risk\_Fraction}}{|\text{Entry\_Price} - \text{SL\_Price}| \times \text{Point\_Value\_Per\_Unit}}$$
   - Contract specifications (`Point_Value_Per_Unit`, minimum lot size, lot step) are parameterized per broker/exchange profile and require explicit verification before use.
2. **Daily Loss Limit:** If cumulative realized + floating daily drawdown reaches the configured Daily Loss Limit (e.g., `2.0%` or `3.0%` in a trading day), the Risk Engine triggers a `DAILY_LOCKOUT` and blocks new `BUY`/`SELL` trade plans until the next daily reset.
3. **Maximum Drawdown Circuit Breaker:** If total equity drawdown from high-water mark reaches the Maximum Drawdown ceiling (e.g., `6.0%` or `8.0%`), the system triggers `MAX_DRAWDOWN_HALT`, requiring manual Founder/user review and reset.
4. **Consecutive Loss Protection:** After $N$ consecutive full-stop losses (e.g., $N = 3$) on a market/timeframe, the engine either enters a mandatory cool-down period or halves the risk per trade by `50%` until a winning trade recovers structure.
5. **Maximum Open Positions & Correlated Risk:**
   - Limits maximum concurrent active trade plans per symbol and across the portfolio.
   - **Correlated Risk Filter:** Because `XAUUSD` and `BTCUSD` can exhibit episodic positive correlation during USD liquidity shocks (e.g., DXY/Fed events), simultaneous same-USD-direction exposure across both markets is capped by a `Max_Combined_USD_Exposure` limit.
6. **Spread & Slippage Protection:**
   - If live bid-ask spread exceeds `max_spread_points` or `max_spread_to_sl_ratio` (e.g., spread $> 15\%$ of total SL distance on `1M`/`5M`), the signal is vetoed (`WAIT — SPREAD_PROTECTION_ACTIVE`).
   - Slippage tolerance parameter recorded on every trade plan so delayed alerts beyond `max_slippage_points` from the confirmed entry zone are marked invalid for execution.
7. **Emergency Stop (Kill Switch):** Instant manual and automated switch in the Founder/Admin Panel and Risk Dashboard that halts all signal emission, webhook dispatches, and active trade plans immediately.
8. **No Initial Live Auto-Trading:** Live order routing to brokers is **disabled** in the initial release. Phase 5 computes complete trade plans, paper-trading simulations, and user notifications while exposing a clean adapter interface for future Founder-approved broker integration.

---

## 16. News Intelligence

Phase 6 monitors macroeconomic and crypto-specific catalysts to provide context and shield the system from erratic news-driven price dislocations. **QUANTUM never fabricates news events, forecast figures, or actual prints.** If the economic calendar feed is disconnected or missing data, the system displays `NOT CONNECTED` or `DATA UNAVAILABLE`.

### 16.1 Macroeconomic & Event Intelligence Matrix

| Event / Indicator | Target Impact | Data Tracked | Protection Window Behaviour |
| :--- | :--- | :--- | :--- |
| **CPI (Consumer Price Index — US)** | Tier-1 High Impact (`XAUUSD` & `BTCUSD`) | Scheduled UTC timestamp, Previous, Consensus Forecast, Actual Print, Surprise Delta ($\text{Actual} - \text{Forecast}$), Source Reliability Score | Pre-event freeze (e.g., `-30 min`) + post-event stabilization quarantine (`+15 to +30 min` + volatility normalization check) |
| **NFP (Non-Farm Payrolls) & Unemployment Rate** | Tier-1 High Impact (`XAUUSD` & `BTCUSD`) | Payrolls change, Unemployment %, Average Hourly Earnings, UTC timestamp | Pre-event freeze + post-event quarantine until spread & ATR stabilize |
| **FOMC Rate Decisions, Statement, & Press Conference** | Tier-1 Critical Impact (`XAUUSD` & `BTCUSD`) | Fed Funds Rate decision, Dot Plot / Statement release (`14:00 America/New_York` — `18:00 UTC` EDT / `19:00 UTC` EST), Powell Press Conference (`+30 min`) | Extended freeze across both the rate release and the duration of the FOMC Press Conference |
| **PCE (Personal Consumption Expenditures — Core PCE)** | Tier-1 High Impact (`XAUUSD` & `BTCUSD`) | MoM / YoY Core PCE actual vs. forecast | Pre-event and post-event protection window |
| **GDP (US Gross Domestic Product — Advance/Prelim/Final)** | Tier-1 / Tier-2 High Impact | QoQ Annualized GDP print vs. forecast | Pre-event and post-event protection window |
| **Initial Jobless Claims / ISM PMI / Retail Sales** | Tier-2 Medium-High Impact | Actual vs. forecast + timestamp | Configurable intraday scalper protection window (`1M`–`15M`) |

### 16.2 Market-Specific Fundamental & Sentiment Intelligence

#### Gold-Specific (`XAUUSD`) Intelligence
- **USD Strength Proxy (DXY):** Monitors inverse directional pressure when a verified DXY feed is connected (shows `NOT CONNECTED` if unconfigured).
- **Federal Reserve Policy & Treasury Yields:** Tracks scheduled Fed speaker calendars, FOMC minutes, and US 10-Year / 2-Year Treasury Yield movements where feed data is available.
- **Inflation & Employment Surprise Tracking:** Classifies macro prints as `HAWKISH_USD_BEARISH_GOLD`, `DOVISH_USD_BULLISH_GOLD`, or `INLINE_NEUTRAL` strictly based on verified `Actual vs. Forecast` delta after the post-news volatility quarantine clears.

#### Bitcoin-Specific (`BTCUSD`) Intelligence
- **Regulatory & SEC / Government Announcements:** High-impact alert tagging for verified regulatory headlines.
- **Spot BTC ETF Developments & Flow Windows:** Awareness of US equity market open/close ETF rebalancing windows (`09:30` and `16:00 America/New_York`).
- **Exchange Events & Outages:** Exchange maintenance, halt warnings, or major exchange security incidents.
- **Perpetual Funding Rates & Open Interest / Liquidation Data (Where Available):** When connected to a verified crypto derivatives data endpoint (e.g., Binance/Bybit/Coinalyze API), tracks extreme positive/negative funding rates and liquidation spikes as sweep confluence. If not connected, explicitly displays `NOT CONNECTED`.

### 16.3 News Provider Disconnect, Stale Calendar, and Fail-Closed Protection Policy
A critical safety rule of QUANTUM is that **missing or disconnected news data must NEVER be treated as confirmation that no news risk exists** ("absence of evidence is not evidence of safety"):
1. **Local Pre-Cached Weekly Schedule & Heartbeat Verification:**
   - The `news_protection` service syncs the upcoming 14-day macroeconomic schedule every 1 hour and checks live actual-print / breaking-event feeds every 60 seconds during active US/London release hours (`07:00–20:00 America/New_York`).
   - All pre-scheduled Tier-1 events (`CPI`, `NFP`, `FOMC`, `PCE`, `GDP`) cached in `news_events` remain strictly enforced even if the live news provider subsequently disconnects.
2. **Tiered Behavior When News Provider Disconnects or Becomes Stale:**
   - **Case 1 — Cached Calendar Valid (`age <= 24h`) AND Outside US Macro Release Windows:** If the live news feed disconnects momentarily while a verified `< 24h` cached schedule shows zero events within the next 2 hours, normal evaluation is permitted **only** if a secondary fallback calendar source or pre-cached schedule is verified; meanwhile the UI badges `NEWS_FEED_DEGRADED_USING_VERIFIED_CACHE`. If the current time enters any standard US Tier-1 macro release window (`08:15–09:00 America/New_York`, `09:45–10:30 America/New_York`, or `13:45–15:00 America/New_York`) while the live feed is disconnected, intraday signals (`1M`–`1H`) are **automatically blocked (`WAIT — NEWS_FEED_UNVERIFIED_DURING_RELEASE_WINDOW`)**.
   - **Case 2 — News Provider Completely Disconnected (`NOT_CONNECTED`) or Calendar Cache Stale (`age > 24h`) or Missing (`DATA_UNAVAILABLE`):**
     - **Strict Fail-Closed Default:** In `STRICT` production mode, Gate 2 **blocks all new `BUY` and `SELL` signals on intraday and swing timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`) and forces the decision to `WAIT`** with `signal_status = 'VETOED_BY_PROTECTION'` and explanation `"Gate 2 Veto: Economic news calendar feed is NOT_CONNECTED / DATA_UNAVAILABLE; fail-closed protection active to prevent blind execution into unmonitored macro events."`
     - **Founder-Only Emergency Override:** Only an explicit, time-bounded (`max 4 hours`), audit-logged Founder override token (`allow_degraded_no_news_override = TRUE` in `system_settings`) can permit signal evaluation during a prolonged third-party news API outage, and every signal emitted under that override is permanently badged `DEGRADED_NO_NEWS_VERIFICATION` and capped at maximum quality grade `B`.

---

## 17. Market Protection System

The Market Protection System acts as an unconditional circuit breaker (`Gate 2` of the Master Decision Engine) that overrides all 12 brains and forces the platform output to **`WAIT`** whenever market microstructure or data freshness degrades.

### 17.1 Circuit-Breaker Triggers & Recovery Matrix

| Protection Trigger | Detection Condition | Automated System Action | Recovery Validation Rule |
| :--- | :--- | :--- | :--- |
| **High-Impact News Window** | Current UTC time falls within `[T_event - pre_window, T_event + post_window]` for any active Tier-1 event. | Force `WAIT`; badge dashboard with `NEWS_PROTECTION_ACTIVE` + live event countdown timer. | Time must pass `T_event + post_window` AND last 3 confirmed `1M`/`5M` bars must return within normal spread and ATR limits. |
| **News Feed Disconnected / Unverified** | News calendar cache stale (`> 24h`), uninitialized (`NOT_CONNECTED` / `DATA_UNAVAILABLE`), or disconnected during US release windows (`08:15–10:30` / `13:45–15:00 America/New_York`). | **Fail-Closed Veto:** Force `WAIT` (`VETOED_BY_PROTECTION`); never assume "no news = safe". | Live news provider reconnects, calendar sync completes, and upcoming 24h event schedule is verified healthy. |
| **Abnormal Volatility Shock** | Single candle range $> 3.5 \times \text{ATR}(14)$ or `ATR_PR > 97.00th` percentile shock. | Force `WAIT`; suspend new entries on affected timeframe. | Volatility ratio must cool below recovery hysteresis threshold (`ATR_PR <= 92.00`) for $M$ consecutive confirmed bars. |
| **Spread Spike** | Live `Ask - Bid > max_allowed_spread` (or $> \theta\%$ of candidate SL distance). | Force `WAIT`; flag `SPREAD_SPIKE_DETECTED`. | Rolling 60-second average spread must drop back below normal threshold. |
| **Low Liquidity / Rollover Dead Zone** | `XAUUSD` daily rollover break (`16:45–18:15 America/New_York`), scheduled market closure/holiday, or volume below minimum floor. | Force `WAIT` on intraday timeframes (`1M`–`1H`). | Active trading session resumes with confirmed candle volume above floor. |
| **Calendar-Aware Stale Data** | Active market session is `OPEN` (per Section 17.2 Market Calendar Engine) AND latest confirmed candle timestamp lags current expected close boundary by more than `grace_seconds`. | Force `WAIT`; display `DATA UNAVAILABLE — STALE FEED`. | Fresh confirmed candles must be ingested, validated, and gap-checked. |
| **Feed Failure / Disconnection** | WebSocket/REST market data provider returns HTTP 5xx, timeout, or socket disconnect during open market hours. | Force `WAIT`; display `NOT CONNECTED`; trigger admin alert. | Provider health check passes, backfill completes any missing historical candles, and continuity check verifies zero gaps. |

### 17.2 Market-Calendar-Aware Stale Data Detection (`XAUUSD` vs. `BTCUSD`)
A naive stale-data check (`now_utc - last_candle_close > timeframe_seconds + grace_seconds`) fails during weekends, daily Gold rollover breaks, and holidays—causing false `STALE FEED` alarms when the market is legitimately closed, or failing to distinguish a closed market from a broken feed. QUANTUM implements a **Market-Calendar-Aware Freshness Engine**:

1. **Separate Market Schedule Calendars:**
   - **`BTCUSD` Calendar (`24/7/365_CONTINUOUS`):**
     - Market State is always `MARKET_OPEN` (except during explicitly announced provider maintenance windows logged in `market_data_status`).
     - **Stale Rule for `BTCUSD`:** Let $T_{\text{expected\_close}}(\text{tf}, t_{\text{now}})$ be the most recent timeframe boundary timestamp $\le t_{\text{now}}$ (using calendar-month boundary math for `1MO`, Monday `00:00 UTC` for `1W`, `00:00 UTC` for `1D`, and modulo seconds for `1M`–`4H`). If $t_{\text{now}} > T_{\text{expected\_close}} + \delta_{\text{grace}}(\text{tf})$ and no confirmed candle with `close_timestamp == T_expected_close` exists in `market_candles`, `BTCUSD` is immediately flagged **`STALE` (`DATA UNAVAILABLE — STALE FEED`)** and Gate 1 forces **`WAIT`**.
   - **`XAUUSD` Calendar (`CME_BULLION_NY_SCHEDULE` via `America/New_York`):**
     - **Weekly Market Close (`MARKET_CLOSED_WEEKEND`):** Friday `17:00:00 America/New_York` through Sunday `18:00:00 America/New_York`.
     - **Daily Rollover Maintenance Break (`MARKET_PAUSED_DAILY_ROLLOVER`):** Monday through Thursday `17:00:00 to 18:00:00 America/New_York`.
     - **Exchange Holiday Schedule (`MARKET_CLOSED_HOLIDAY`):** Good Friday, Christmas Day, New Year's Day, and early-close US holiday schedules (`13:00` or `14:30 America/New_York` early close on Thanksgiving, Independence Day, etc.) loaded from the verified exchange holiday calendar.
     - **Stale Rule for `XAUUSD`:**
       - When `XAUUSD` calendar state is `MARKET_CLOSED_WEEKEND`, `MARKET_PAUSED_DAILY_ROLLOVER`, or `MARKET_CLOSED_HOLIDAY`:
         - No new intraday candles are expected during the closed interval.
         - The system status is explicitly set to **`MARKET_CLOSED` (NOT `STALE`)**, preventing false stale-data error alerts.
         - However, Gate 1 & Gate 2 still force all live decision outputs to **`WAIT` (`REASON: XAUUSD_MARKET_CLOSED`)** so old Friday or pre-rollover signals can never be re-emitted as fresh live signals while the market is closed.
       - When `XAUUSD` calendar state is **`MARKET_OPEN`**:
         - Any confirmed candle close boundary $T_{\text{expected\_close}}$ falling inside `MARKET_OPEN` hours that is not ingested within $\delta_{\text{grace}}(\text{tf})$ (e.g., `10s` for `1M`–`15M`, `30s` for `30M`–`4H`, `60s` for `1D`–`1MO`) immediately triggers **`STALE` (`DATA UNAVAILABLE — STALE FEED`)**, blocks all brain evaluations, and forces **`WAIT`**.
       - **Session Re-Open Verification Gate:** At Sunday `18:00 America/New_York` (or daily `18:00 America/New_York` after rollover), `XAUUSD` remains in `REOPEN_WARMUP_WAIT` until the first new confirmed candle of the reopened session is ingested and verified, preventing stale pre-close data from triggering orders on the opening gap.

---

## 18. Website Architecture & UI/UX Design System

### 18.1 Three UI Design Concepts for Founder Selection

**Theme status:** `PENDING FOUNDER DECISION`. No theme will be finalized in code until the Founder selects Concept A, Concept B, or Concept C.

#### Concept A: Black + Gold — Premium Institutional
- **Visual Persona:** Private Swiss bullion bank meets institutional multi-asset execution desk. Authoritative, restrained, high-contrast luxury precision.
- **Color Tokens:**
  - Background Primary: `#08080A` (Obsidian Carbon)
  - Background Elevated / Card: `#111216` (Institutional Slate)
  - Border / Hairline: `#23242C` (Muted Titanium) / `#3D321C` (Subtle Gold Edge)
  - Accent Primary: `#D4AF37` (Metallic Sovereign Gold) & `#F3E5AB` (Champagne Highlight)
  - Semantic Buy / Bullish: `#10B981` (Emerald Institutional Green)
  - Semantic Sell / Bearish: `#EF4444` (Crimson Risk Red)
  - Semantic Wait / Neutral: `#D97706` (Amber Caution) / `#9CA3AF` (Neutral Silver)
  - Text Primary / Secondary: `#F9FAFB` / `#9CA3AF`

#### Concept B: Black + Electric Blue — Futuristic AI
- **Visual Persona:** High-frequency quantitative research lab and autonomous neural telemetry command center. Crisp, analytical, high-density optical clarity.
- **Color Tokens:**
  - Background Primary: `#050811` (Deep Abyss Navy-Black)
  - Background Elevated / Card: `#0B1120` (Quantum Midnight Panel)
  - Border / Hairline: `#1E293B` (Slate Grid) / `#1D4ED8` (Active Electric Focus)
  - Accent Primary: `#00E5FF` (Electric Cyan) & `#3B82F6` (Cobalt Intelligence Blue)
  - Semantic Buy / Bullish: `#00F5A0` (Bio-Teal Green)
  - Semantic Sell / Bearish: `#FF3366` (Laser Rose Red)
  - Semantic Wait / Neutral: `#F59E0B` (Signal Amber) / `#94A3B8` (Cool Slate)
  - Text Primary / Secondary: `#F8FAFC` / `#94A3B8`

#### Concept C: Black + Neon Green — Trading Terminal
- **Visual Persona:** Classic institutional Bloomberg/proprietary floor terminal re-engineered for modern low-latency SMC price action. Zero distraction, maximum tabular scan speed.
- **Color Tokens:**
  - Background Primary: `#050605` (Terminal Pitch Black)
  - Background Elevated / Card: `#0C0F0D` (Matrix Charcoal)
  - Border / Hairline: `#1A241E` (Phosphor Grid Line)
  - Accent Primary: `#00FF66` (Terminal Neon Green) & `#A3E635` (Lime Vector)
  - Semantic Buy / Bullish: `#00FF66` (High-Luminance Green)
  - Semantic Sell / Bearish: `#FF3B30` (Terminal Alert Red)
  - Semantic Wait / Neutral: `#FFCC00` (Terminal Warning Yellow) / `#71717A` (Zinc Gray)
  - Text Primary / Secondary: `#ECFDF5` / `#86EFAC` (Monospace data labels) & `#A1A1AA`

### 18.2 Shared Design System & Component Standards
- **Typography:**
  - UI & Analytical Headers: Geometric Sans-Serif (`Inter` or `Plus Jakarta Sans`), weights `500, 600, 700`.
  - Prices, Timestamps, Votes, R:R Ratios, P&L Tables: Strict Tabular Monospace (`JetBrains Mono` or `IBM Plex Mono` with `font-variant-numeric: tabular-nums`) so digits never jitter during live tick updates.
- **Core Component Library Specifications:**
  - **Buttons:** Primary Action, Secondary Outline, Danger/Emergency Stop (requires 2-step confirmation modal), Timeframe Selector Group (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`), and Mode Toggle (`Mode A: Independent` vs. `Mode B: MTF Confirmed`).
  - **Inputs & Controls:** Validated numeric inputs for Account Equity, Risk %, and Strategy Lab parameters with inline min/max/step guardrails.
  - **Tables:** High-density virtualized data tables for Signal History, 12-Brain Audit Matrix, and Backtest Ledger with column sorting, market/timeframe filtering, and CSV/JSON export.
  - **Cards & Panels:** 1px crisp borders, zero decorative clutter; every card displays its active `Symbol`, `Timeframe`, `Last Confirmed Close UTC`, and `Data Status Badge`.
  - **Modals & Drawers:** Signal Deep-Dive Drawer (shows full 12-brain reasoning JSON + chart snapshot levels) and Founder Approval / Emergency Stop Confirmation Modals.
  - **Tooltips:** Explain exact technical definitions (e.g., hovering `Consequent Encroachment` or `Brain 5 Confidence` shows the exact formula and current values).
  - **Charts:** TradingView Lightweight Charts canvas with custom multi-pane overlays for `BOS`/`CHoCH`/`MSS` lines, `OB`/`BB`/`FVG` shaded rectangles, `BSL`/`SSL`/`PDH`/`PDL` horizontal rays, and `Entry`/`SL`/`TP1`/`TP2`/`TP3` risk-reward projection boxes.
- **Mandatory UI States:**
  - **Loading State:** Structured skeleton loaders matching exact card geometry.
  - **Empty State:** Clear explanatory notice (e.g., `"No confirmed BUY/SELL signals matched the current filter criteria"`).
  - **Error / Disconnected State:** High-visibility banner displaying `DATA UNAVAILABLE` or `NOT CONNECTED` with last known healthy timestamp and retry status.
- **Responsive Layout & Accessibility:**
  - **Desktop Layout (`>= 1280px`):** Multi-panel command workstation (Top Market/Timeframe/Protection Bar, Center Chart + Trade Plan, Right 12-Brain & Decision Matrix, Bottom MTF/SMC/History Tabs).
  - **Mobile/Tablet Layout (`< 1024px`):** Collapsible navigation drawer, sticky Market + 9-Timeframe selector bar, stacked priority cards (Master Decision & Protection Status first, followed by Chart, 12-Brain Accordion, and Risk Plan).
  - **Accessibility:** WCAG 2.1 AA contrast ratios (`>= 4.5:1`), full keyboard navigation, `aria-live` announcements for confirmed signal emissions, and colorblind-safe directional icons (`▲ BUY`, `▼ SELL`, `■ WAIT`) alongside color coding.

### 18.3 Complete Website Sitemap (18 Core Modules)

| # | Module / Route | Primary Purpose & Functional Scope | Role Access |
| :--- | :--- | :--- | :--- |
| **1** | **Main Dashboard** (`/dashboard`) | Executive command center showing active Master Decisions for `XAUUSD` and `BTCUSD`, active timeframe selector, protection status, and latest confirmed signals. | All Authenticated Roles |
| **2** | **Market Overview** (`/markets`) | Side-by-side comparison of `XAUUSD` and `BTCUSD` across all 9 timeframes (`9x2` heat grid showing trend, structure, volatility regime, and active decision). | All Authenticated Roles |
| **3** | **XAUUSD Dedicated Dashboard** (`/markets/xauusd`) | Gold-focused workspace with NY/London/Asian session liquidity tracker, PDH/PDL/PWH/PWL levels, macro calendar countdown, and Gold 9-timeframe selector. | All Authenticated Roles |
| **4** | **BTCUSD Dedicated Dashboard** (`/markets/btcusd`) | Bitcoin-focused workspace with 24/7 UTC structure, crypto news/ETF/funding telemetry (where connected), and Bitcoin 9-timeframe selector. | All Authenticated Roles |
| **5** | **Live Interactive Chart** (`/chart`) | Full-screen TradingView Lightweight Charts workspace with selectable SMC overlays (`OB`, `FVG`, `BOS/MSS`, `EQH/EQL`, `Dealing Range`) and active trade plan overlay. | All Authenticated Roles |
| **6** | **12-Brain Intelligence Dashboard** (`/brains`) | Real-time & historical inspection of all 12 brains: individual vote (`BUY`/`SELL`/`NEUTRAL`/`ABSTAIN`), confidence bar (`0–100%`), raw calculated metrics, and text explanation. | All Authenticated Roles |
| **7** | **SMC Intelligence Dashboard** (`/smc`) | Complete registry of active & mitigated Order Blocks, Breaker Blocks, FVGs, IFVGs, Liquidity Pools (`BSL`/`SSL`), Sweeps, and Dealing Range Premium/Discount gauges. | All Authenticated Roles |
| **8** | **Multi-Timeframe (MTF) Dashboard** (`/mtf`) | Synchronized 9-timeframe matrix (`1M` to `1MO`) displaying Trend, Structure, Liquidity Draw, POI location, and Mode B conflict diagnostics. | All Authenticated Roles |
| **9** | **Master Decision Dashboard** (`/decisions`) | Deep-dive inspector into the Phase 4 Decision Engine showing Gate 1–6 pass/fail telemetry, vote tally, signal quality grade (`A+`, `A`, `B`, `WAIT`), and full explanation log. | All Authenticated Roles |
| **10** | **News & Market Protection Dashboard** (`/news-protection`) | Economic calendar (CPI, NFP, FOMC, PCE, GDP), actual vs. forecast tracker, Gold/BTC catalyst monitor, spread/volatility circuit-breaker status, and protection quarantine timer. | All Authenticated Roles |
| **11** | **Signal History & Audit Ledger** (`/signals/history`) | Immutable historical log of every emitted signal filtered by Symbol, Timeframe (`1M`–`1MO`), Mode (`A` vs. `B`), Direction, and Outcome (`TP1/2/3`, `SL`, `Expired`). | All Authenticated Roles |
| **12** | **Risk Management & Position Calculator** (`/risk`) | Interactive trade planner computing exact lot/unit size from user equity & risk %, plus tracking Daily Loss Limit, Max Drawdown, Consecutive Losses, and Emergency Stop state. | All Authenticated Roles |
| **13** | **Performance Analytics** (`/analytics`) | Verified performance metrics segmented strictly by Market, Timeframe (`1M`–`1MO`), and Signal Mode: Win Rate, Profit Factor, Expectancy, Avg R, Max Drawdown, Recovery Factor. | All Authenticated Roles (Scoped by Tier) |
| **14** | **Strategy Lab** (`/strategy-lab`) | Sandbox for testing timeframe-specific parameter profiles, running historical backtests, walk-forward analyses, and comparing strategy versions prior to Founder approval. | Founder, Admin, Private Tester |
| **15** | **Account Settings** (`/settings`) | User profile, password/MFA security, default timeframe preference, timezone display preference, and paper-account risk baseline. | All Authenticated Roles |
| **16** | **Notifications Center** (`/notifications`) | In-app notification feed and webhook/alert subscription preferences per symbol and timeframe (`1M`–`1MO`). | All Authenticated Roles |
| **17** | **Admin Panel** (`/admin`) | User management, tester invitation codes, data provider health monitoring, system/API logs, and audit log viewer (cannot override Founder locks). | Admin, Founder |
| **18** | **Founder Control Panel** (`/founder`) | Exclusive governance console: Phase approval gates, locked configuration overrides, strategy version promotion, public launch toggle, and system-wide Emergency Stop control. | **Founder Only** |

---

## 19. TradingView & Pine Script v6 Integration

Phase 7 includes a synchronized **TradingView Pine Script v6** integration (`//@version=6`).

### 19.1 Pine Script v6 Architectural Specification & Non-Repainting MTF Logic
- **Purpose:** Allow traders to visualize QUANTUM's non-repainting structure, SMC zones, 12-Brain summary dashboard, and confirmed `BUY`/`SELL`/`WAIT` signals directly on TradingView charts across `XAUUSD` and `BTCUSD` on all 9 timeframes, and dispatch authenticated webhook alerts to the QUANTUM backend.
- **Canonical Internal-to-Pine Script v6 Timeframe Mapping (`f_to_pine_tf` & `f_to_quantum_tf`):**
  - Because Pine Script uses `"1"` for 1 Minute and `"1M"` for 1 Month whereas QUANTUM uses `"1M"` for 1 Minute and `"1MO"` for 1 Month, all Pine Script code and webhook serializers must enforce the bidirectional mapping defined in Section 6.2:
    ```pine
    //@version=6
    // Converts QUANTUM Internal Timeframe Enum ('1M'..'1MO') to Pine Script timeframe.period string
    f_quantum_to_pine_tf(string q_tf) =>
        switch q_tf
            "1M"  => "1"
            "5M"  => "5"
            "15M" => "15"
            "30M" => "30"
            "1H"  => "60"
            "4H"  => "240"
            "1D"  => "1D"
            "1W"  => "1W"
            "1MO" => "1M"
            => ""

    // Converts Pine Script timeframe.period to QUANTUM Internal Timeframe Enum ('1M'..'1MO')
    f_pine_to_quantum_tf(string p_tf) =>
        switch p_tf
            "1"   => "1M"
            "5"   => "5M"
            "15"  => "15M"
            "30"  => "30M"
            "60"  => "1H"
            "240" => "4H"
            "1D"  => "1D"
            "D"   => "1D"
            "1W"  => "1W"
            "W"   => "1W"
            "1M"  => "1MO"
            "M"   => "1MO"
            => "UNSUPPORTED_TF"
    ```
- **Strict Non-Repainting Engineering Rules in Pine Script v6 (Confirmed HTF vs. Developing HTF):**
  1. **Why Naive `request.security(..., expression, lookahead = barmerge.lookahead_off)` Still Repaints Intrabar / Causes Historical-vs-Realtime Discrepancy:**
     - In Pine Script, calling `request.security(syminfo.tickerid, htf_pine_tf, close, lookahead = barmerge.lookahead_off)` returns the last *closed* HTF bar on historical bars, **but on live real-time bars** it returns the *currently developing (unclosed)* HTF candle's live value! Furthermore, if an expression is evaluated inside the HTF context without indexing `[1]` (or without gating on `barstate.isconfirmed`), historical bars align the HTF bar's final close to the beginning or end of the HTF period differently than real-time execution.
  2. **Mandatory Confirmed-HTF Retrieval Pattern (`[1]` Closed-Bar Tuple + `barmerge.lookahead_on` or Confirmed-Close Gating):**
     - According to TradingView's official Pine Script v6 non-repainting specification, to retrieve **strictly the most recently completed (`is_confirmed == TRUE`) HTF candle** identically across both historical backtest bars and live real-time streaming bars—with zero future leakage and zero developing-bar contamination—every HTF data or indicator tuple must be offset by `[1]` inside the `request.security()` expression and paired with `lookahead = barmerge.lookahead_on` (which in Pine Script specifically prevents the `[1]` offset from being delayed by an extra HTF period on historical bars while never reading the `[0]` developing bar), **OR** evaluated via a dedicated HTF confirmation latch:
     ```pine
     // Canonical Non-Repainting Confirmed HTF Tuple Retrieval in Pine Script v6
     // Indexing [1] inside the tuple guarantees ONLY the already-closed HTF bar is read.
     f_get_confirmed_htf_state(string htf_pine_tf) =>
         if htf_pine_tf == ""
             [float(na), float(na), float(na), float(na), float(na), int(na), false]
         else
             request.security(
                 syminfo.tickerid,
                 htf_pine_tf,
                 [open[1], high[1], low[1], close[1], volume[1], time_close[1], barstate.isconfirmed[1]],
                 gaps = barmerge.gaps_off,
                 lookahead = barmerge.lookahead_on
             )
     ```
  3. **Timestamp Cutoff Verification (`htf_time_close <= time_close`):**
     - After retrieving `htf_time_close` (`time_close[1]` of the HTF bar), the script explicitly asserts `not na(htf_time_close) and htf_time_close <= time_close`.
     - **Developing HTF Candles Excluded:** The developing HTF candle (`index [0]` on the HTF) is completely excluded from all Brain 2, MTF, and Master Decision calculations. It may optionally be displayed in the heads-up dashboard table strictly labeled as `DEVELOPING (UNCONFIRMED — NOT USED FOR VOTING)`.
  4. **Execution-Bar Confirmation Gate (`barstate.isconfirmed`):**
     - All execution-timeframe signal decisions, state transitions, and `alert()` webhook dispatches execute strictly inside `if barstate.isconfirmed`. Intrabar (unconfirmed tick) signals are never emitted.
  5. **Handling Missing, `na`, or Top-of-Hierarchy (`1MO`) HTF Data:**
     - If `q_tf == "1MO"` (`htf1_pine_tf == ""` and `htf2_pine_tf == ""`), Brain 2 follows the Section 9.2 / Section 11.2 rule (`TOP_OF_HIERARCHY_NO_HTF`, `vote = 'NEUTRAL'`).
     - If `q_tf == "1W"` (`htf1_pine_tf == "1M"` [Monthly] and `htf2_pine_tf == ""`), Brain 2 evaluates `HTF 1` at `100%` weight.
     - For any mapped HTF where `htf_pine_tf != ""`, if `na(htf_close)` or `na(htf_ema200)` (e.g., insufficient historical HTF bars loaded on TradingView chart), Brain 2 outputs `ABSTAIN_DATA_UNAVAILABLE`, the on-chart table renders `DATA UNAVAILABLE`, and in Mode B (`MTF_CONFIRMED`) the Master Decision is forced to `WAIT`.
- **Visual On-Chart Components:**
  - Confirmed `BUY` and `SELL` signal labels with Entry, `SL`, `TP1`, `TP2`, and `TP3` price lines and shaded R:R projection boxes.
  - SMC Overlays: Active Bullish/Bearish Order Blocks (with 50% Mean Threshold line), Breaker Blocks, Mitigation Blocks, Fair Value Gaps (with 50% Consequent Encroachment line), `BOS`/`CHoCH`/`MSS` structural break lines, `EQH`/`EQL` liquidity tags, and `PDH`/`PDL`/`PWH`/`PWL` rays.
  - On-Chart Heads-Up Table (`table.new`): Displays active Market, Execution Timeframe (`1M`–`1MO`), Signal Mode (`Mode A` vs. `Mode B`), Master Decision (`BUY` / `SELL` / `WAIT`), Quality Grade (`A+` / `A` / `B` / `WAIT`), Brain Vote Tally (`e.g., 9 BUY / 0 SELL / 3 NEUTRAL`), Aggregate Confidence %, Active Session, Spread/Volatility Warning, and Strategy Version.
- **Webhook Payload Contract & Platform Limitations:**
  - **18-Field Canonical Webhook JSON:** When `barstate.isconfirmed` is true on a state change or confirmed signal, Pine Script serializes a JSON alert containing all 18 mandatory signal attributes (Section 14.3) plus `webhook_secret`, `event_nonce` (`symbol + "_" + execution_timeframe + "_" + str.tostring(time_close) + "_" + direction`), and `pine_script_version`.
  - **No Arbitrary Outbound HTTP Calls:** Pine Script cannot execute arbitrary `fetch()` or pull external REST APIs (such as live macroeconomic news feeds) directly inside the script.
  - **Outbound Alerts Only:** Pine Script communicates outward exclusively via TradingView's native `alert()` mechanism sending the structured JSON payload to `POST /api/v1/webhooks/tradingview`.
  - **Execution & Drawing Limits:** Pine Script v6 enforces compilation limits on drawing objects (`max_boxes_count = 500`, `max_lines_count = 500`, `max_labels_count = 500`), execution time, and `request.security()` call count (max 40 calls). Therefore, the Pine Script indicator bundles all HTF series per timeframe into a single tuple `request.security()` call (using at most 2 `request.security()` calls total: one for `HTF 1` and one for `HTF 2`), while the Python backend performs full 9-timeframe concurrent cross-computations and Phase 6 News Protection filtering on incoming webhooks.

---

## 20. Frontend Architecture

### 20.1 Technology Evaluation & Architectural Design

| Technology | Purpose in QUANTUM | Suitability & Strengths | Alternatives Considered | Limitations & Cost Verification |
| :--- | :--- | :--- | :--- | :--- |
| **Next.js (App Router) / React 19** | Core web application framework, SSR/CSR hybrid rendering, role-protected routing. | Industry-standard React framework with strong layout composition, middleware auth guards, and streaming UI performance. | Vite + React SPA (currently scaffolded in root workspace; migration or full-stack pairing decided in Phase 0). | Open-source (MIT, $0 license cost). Self-hosted via Docker incurs zero framework fee. |
| **TypeScript** | Strict static type checking across all frontend models, API contracts, and 9-timeframe enums. | Eliminates runtime type errors; guarantees `1M` vs. `1MO` and `SignalPayload` contract safety. | JavaScript (Rejected: lacks compile-time safety for financial calculations). | Open-source (Apache 2.0, $0). |
| **Tailwind CSS** | Utility-first styling engine implementing the selected Founder UI Theme (Concept A, B, or C) via CSS design tokens. | Zero runtime CSS-in-JS overhead; ideal for high-density dark-mode trading terminals. | Vanilla CSS Modules / Styled Components. | Open-source (MIT, $0). |
| **TradingView Lightweight Charts** | High-performance HTML5 Canvas financial charting library for OHLCV candles and custom SMC primitives. | Free, open-source (Apache 2.0) canvas engine rendering tens of thousands of candles at 60 FPS with custom plugin primitives for OB/FVG boxes. | TradingView Advanced Charting Library (Requires commercial brokerage/public website license verification — not assumed available). | Lightweight Charts is free & open-source ($0, requires attribution link per Apache 2.0 license). Does not include built-in indicators; QUANTUM renders all overlays directly from backend calculations. |
| **WebSockets (Native / Reconnecting Client)** | Real-time push stream for confirmed candle closes, 12-brain telemetry updates, and protection alerts. | Eliminates polling lag on `1M` and `5M` timeframes; supports automatic heartbeat and state reconciliation on reconnect. | Server-Sent Events (SSE) or HTTP Polling (Fallback only). | Native browser standard ($0). |

---

## 21. Backend Architecture

### 21.1 Technology Evaluation & Service Design

| Technology | Purpose in QUANTUM | Suitability & Strengths | Alternatives Considered | Limitations & Cost Verification |
| :--- | :--- | :--- | :--- | :--- |
| **Python FastAPI** | High-performance asynchronous REST and WebSocket API server + core quantitative intelligence execution host. | Native async/await support, automatic OpenAPI schema generation, seamless integration with Python's numerical ecosystem (`numpy`, `pandas`, `polars`). | Node.js / Express (TypeScript) or Go. (Python is superior for multi-brain quantitative vector math and walk-forward backtesting). | Open-source (MIT, $0). CPU-bound backtests must run in worker processes to avoid blocking the async event loop. |
| **Pydantic v2** | Strict runtime data validation and serialization for market candles, brain outputs, and signal schemas. | Rust-backed validation speed; enforces strict invariants (`high >= low`, `confidence in [0,100]`, timeframe enum validation). | Marshmallow / dataclasses. | Open-source (MIT, $0). |
| **SQLAlchemy 2.0 + Alembic** | Async ORM / SQL query builder (`SQLAlchemy`) and version-controlled database schema migration engine (`Alembic`). | Supports strongly typed async PostgreSQL/TimescaleDB queries and auditable, reversible schema migrations across Phases 0–9. | Prisma / Raw `asyncpg`. | Open-source (MIT, $0). |
| **Redis** | In-memory sub-millisecond cache for latest confirmed candle states across `2 markets × 9 timeframes`, pub/sub message broker for WebSockets, rate limiting, and Celery task queue broker. | Essential for low-latency state broadcasting and deduplicating signal evaluation locks. | Memcached / RabbitMQ. | Open-source / Redis Stack ($0 self-hosted in Docker). |
| **Celery** | Distributed task queue and scheduled beat worker for multi-timeframe candle ingestion, 12-brain evaluation pipelines, news polling, and asynchronous historical backtest runs. | Decouples heavy computation and periodic data synchronization from user-facing API latency. | Dramatiq / ARQ / Temporal. | Open-source (BSD, $0). Requires worker monitoring (Flower / Prometheus). |

### 21.2 Backend Modular Service Decomposition
The backend is structured into strictly isolated domain modules:
1. **`ingestion_service`**: Connects to configured market data providers, normalizes `XAUUSD` and `BTCUSD` ticks/candles, validates chronological continuity, constructs or verifies all 9 timeframes (`1M`–`1MO`), and persists confirmed bars.
2. **`smc_service` (Phase 2)**: Computes and updates the 26 institutional SMC features per `(symbol, timeframe)` on every confirmed candle close.
3. **`brains_service` (Phase 1)**: Executes all 12 independent brains in parallel/topological order and collects structured votes and confidence scores.
4. **`mtf_service` (Phase 3)**: Enforces non-repainting timestamp cutoff alignment across the 9 timeframes.
5. **`protection_service` (Phase 6)**: Evaluates economic calendar events, spread spikes, volatility shocks, and feed health.
6. **`decision_engine` (Phase 4)**: Runs the 6-gate `STRICT` mode evaluation to produce the immutable `BUY`, `SELL`, or `WAIT` signal record.
7. **`risk_service` (Phase 5)**: Computes `Entry`, `SL`, `TP1/TP2/TP3`, Position Size, R:R validation, and checks portfolio circuit breakers.
8. **`backtest_service` (Phase 8)**: Event-driven bar-by-bar historical replay engine calling the exact same Phase 1–6 modules used in live production.

---

## 22. Database Architecture & Entity-Relationship Design

### 22.1 Storage Engine Evaluation: PostgreSQL + TimescaleDB & Hypertable Partitioning Rules
- **PostgreSQL 16+:** Primary ACID-compliant relational database for users, RBAC permissions, system configurations, audit logs, strategy versions, and signal records. (Open-source, PostgreSQL License, $0).
- **TimescaleDB Extension & Mandatory Partitioning Key Invariant:**
  - **TimescaleDB Architectural Requirement:** In TimescaleDB, any table converted into a time-partitioned **hypertable** via `create_hypertable(table_name, time_column_name)` **must include the time-partitioning column (`timestamp`, `candle_timestamp`, or `created_at`) in EVERY `PRIMARY KEY` and EVERY `UNIQUE` index/constraint** on that table. Furthermore, standard PostgreSQL `FOREIGN KEY` constraints **cannot reference a single-column `id (UUID)` on a hypertable** because a hypertable cannot have a single-column `UNIQUE (id)` index without the partitioning timestamp column.
  - **Explicit Classification of All 31 Tables (3 TimescaleDB Hypertables vs. 28 Regular PostgreSQL Relational Tables):**
    - **TimescaleDB Hypertables (3 High-Volume Time-Series Tables):**
      1. `market_candles` — Partitioned on `timestamp (TIMESTAMPTZ)` (`chunk_time_interval = INTERVAL '7 days'`). Composite PK: `(symbol_id, timeframe, timestamp)`. No incoming foreign keys from other tables.
      2. `system_logs` — Partitioned on `created_at (TIMESTAMPTZ)` (`chunk_time_interval = INTERVAL '7 days'`). Composite PK: `(created_at, id)`. No incoming foreign keys.
      3. `api_logs` — Partitioned on `created_at (TIMESTAMPTZ)` (`chunk_time_interval = INTERVAL '7 days'`). Composite PK: `(created_at, id)`. No incoming foreign keys.
    - **Regular PostgreSQL Relational Tables (28 ACID Relational Tables — Including `brain_analyses`, `brain_votes`, `smc_analyses`, `mtf_analyses`, `signals`, `trade_plans`, `signal_history`, `risk_records`, and `audit_logs`):**
      - **Why `brain_analyses` is a Regular PostgreSQL B-Tree Indexed Table (or Composite-Keyed if Partitioned):** In the original draft, `brain_analyses` was listed as a hypertable while using a single-column `id (UUIDv7 PK)`, a unique index without `created_at`, and being referenced by single-column foreign keys `brain_votes.brain_analysis_id -> brain_analyses(id)` and `signals.brain_analysis_id -> brain_analyses(id)`—which causes `ERROR: cannot create a unique index without the column "<time_column>" (used in partitioning)` during Alembic migration.
      - **Engineered Resolution:**
        - `market_candles`, `system_logs`, and `api_logs` are the **3 dedicated TimescaleDB Hypertables**, all configured with composite primary keys that include their partitioning timestamp column (`(symbol_id, timeframe, timestamp)` and `(created_at, id)`).
        - `brain_analyses`, `brain_votes`, `smc_analyses`, `mtf_analyses`, `signals`, `signal_history`, `trade_plans`, and `risk_records` are maintained as **Regular PostgreSQL 16 Relational Tables** with time-ordered `UUIDv7` primary keys and composite B-Tree indexes on `(symbol_id, timeframe, candle_timestamp DESC)`. This guarantees 100% standard ACID foreign-key integrity (`signals -> brain_analyses(id)`, `brain_votes -> brain_analyses(id)`, `trade_plans -> signals(id)`, `signal_history -> signals(id)`) and zero TimescaleDB unique-index migration errors, while storing only 1 row per confirmed candle evaluation (easily handled by standard PostgreSQL B-Tree indexing for decades of 9-timeframe history).
        - *(Optional High-Scale Partitioning Rule: If `brain_analyses` is ever converted to a hypertable partitioned by `candle_timestamp`, its primary key must be `(candle_timestamp, id)`, its unique constraint must be `(symbol_id, timeframe, candle_timestamp, strategy_version_id)`—which includes `candle_timestamp`—and child tables `brain_votes` and `signals` must reference the composite foreign key `(brain_analysis_candle_timestamp, brain_analysis_id) REFERENCES brain_analyses(candle_timestamp, id)`).*
- **Reconciliation of Table Counts (31 Database Tables vs. 32 Phase 0 Blueprint Documentation Scope Items):**
  - **31 Total Database Tables across the Entire Project:**
    - **20 Phase 0 Foundation, Governance, Market Data & Logging Tables** (Tables `#1` through `#20` in Section 22.3.A).
    - **11 Phase 1–8 Intelligence, Signal, Risk, News & Backtesting Tables** (Tables `#21` through `#31` in Section 22.3.B).
    - All 31 tables are defined in the initial baseline schema/migration plan so foreign-key relationships and Phase 0 schema validation tests verify the entire data model upfront, while Phase 1–8 services populate Tables `#21–#31` only when their respective phases are approved.
  - **32 Phase 0 Blueprint Documentation Items:** Refers to the 32 architectural and documentation deliverables required in Phase 0 planning (covering Vision, Brand, Sitemap, Frontend, Backend, 31-Table DB Schema, Auth, RBAC, 24 Security Controls, Providers, etc. in Section 27), **not** 32 database tables.

### 22.2 Entity-Relationship Diagram (Mermaid)

```mermaid
erDiagram
    users ||--o{ user_roles : "assigned"
    roles ||--o{ user_roles : "grants"
    roles ||--o{ role_permissions : "contains"
    permissions ||--o{ role_permissions : "defines"
    users ||--o{ sessions : "maintains"
    users ||--o{ subscriptions : "holds"
    users ||--o{ notifications : "receives"
    users ||--o{ audit_logs : "generates"
    users ||--o{ founder_approvals : "authorizes"

    market_data_providers ||--o{ market_symbols : "supplies"
    market_symbols ||--o{ market_candles : "records_hypertable"
    market_symbols ||--o{ market_data_status : "monitors"

    project_phases ||--o{ founder_approvals : "requires"
    strategy_versions ||--o{ signals : "governs"
    strategy_versions ||--o{ backtest_runs : "evaluates"

    market_symbols ||--o{ brain_analyses : "analyzed_by"
    brain_analyses ||--o{ brain_votes : "produces_12"
    market_symbols ||--o{ smc_analyses : "maps"
    market_symbols ||--o{ mtf_analyses : "aligns"
    market_symbols ||--o{ news_events : "impacts"

    signals ||--o| trade_plans : "defines_when_buy_or_sell"
    signals ||--o{ signal_history : "tracks_lifecycle"
    signals }o--|| brain_analyses : "references"
    signals }o--|| smc_analyses : "references"
    signals }o--o| mtf_analyses : "references_in_mode_b"
    trade_plans ||--o{ risk_records : "enforces"

    backtest_runs ||--|| performance_metrics : "summarizes"
```

### 22.3 Complete Database Entity Specification (31 Core & Intelligence Tables)

#### A. Foundation, Governance, and Access Control Entities (Phase 0 — 20 Tables: 3 TimescaleDB Hypertables + 17 Regular PostgreSQL Tables)

| # | Table Name | Table Type | Primary Key & Key Columns | Relationships & Constraints | Indexes & Retention Policy |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | `users` | Regular PostgreSQL Table | `id (UUID PK)`, `email (UNIQUE)`, `password_hash`, `full_name`, `mfa_enabled`, `mfa_secret_enc`, `is_active`, `is_verified`, `created_at`, `updated_at` | Referenced by `user_roles`, `sessions`, `audit_logs`. `CHECK (email = lower(email))` | Unique B-Tree on `email`. Retained indefinitely while account exists (soft-delete audit compliant). |
| **2** | `roles` | Regular PostgreSQL Table | `id (UUID PK)`, `code (UNIQUE: 'FOUNDER', 'ADMIN', 'PRIVATE_TESTER', 'FREE_USER', 'PREMIUM_USER')`, `name`, `description`, `is_system_locked` | Referenced by `user_roles`, `role_permissions`. `FOUNDER` role has `is_system_locked = TRUE`. | Unique index on `code`. Permanent retention. |
| **3** | `permissions` | Regular PostgreSQL Table | `id (UUID PK)`, `code (UNIQUE)`, `module`, `description` | Referenced by `role_permissions`. Granular codes (e.g., `phase:approve`, `signals:read:all_tf`, `killswitch:trigger`). | Unique index on `code`, index on `module`. Permanent retention. |
| **4** | `user_roles` | Regular PostgreSQL Table | `user_id (UUID FK)`, `role_id (UUID FK)`, `assigned_by (UUID FK)`, `assigned_at` | Composite PK `(user_id, role_id)`. Cascade on user delete; restrict on role delete. | Index on `user_id` and `role_id`. Permanent audit trail. |
| **5** | `role_permissions` | Regular PostgreSQL Table | `role_id (UUID FK)`, `permission_id (UUID FK)`, `granted_at` | Composite PK `(role_id, permission_id)`. | Index on `role_id`. Permanent retention. |
| **6** | `sessions` | Regular PostgreSQL Table | `id (UUID PK)`, `user_id (UUID FK)`, `token_hash (UNIQUE)`, `ip_address`, `user_agent`, `expires_at`, `revoked_at`, `created_at` | FK to `users(id)`. Never stores raw session tokens, only SHA-256 hash. | Index on `(user_id, expires_at)` and `token_hash`. Purged 90 days after expiry. |
| **7** | `subscriptions` | Regular PostgreSQL Table | `id (UUID PK)`, `user_id (UUID FK)`, `tier_code`, `status ('DISABLED_PRIVATE_BETA', 'ACTIVE', 'EXPIRED')`, `valid_from`, `valid_until` | FK to `users(id)`. Initially locked to private beta invitation tiers until Phase 9 approval. | Index on `(user_id, status)`. Permanent billing/tier audit retention. |
| **8** | `market_symbols` | Regular PostgreSQL Table | `id (UUID PK)`, `symbol (UNIQUE: 'XAUUSD', 'BTCUSD')`, `asset_class`, `tick_size`, `decimal_places`, `contract_size`, `session_timezone_iana`, `daily_close_local_time`, `four_hour_alignment_mode`, `is_active`, `config_json` | Referenced by all market data and intelligence tables. Stores `America/New_York` (`17:00`) for `XAUUSD` and `UTC` (`00:00`) for `BTCUSD`. | Unique index on `symbol`. Permanent retention. |
| **9** | `market_data_providers` | Regular PostgreSQL Table | `id (UUID PK)`, `provider_code (UNIQUE)`, `name`, `supported_symbols`, `priority_rank`, `rate_limit_rpm`, `is_enabled`, `connection_status ('NOT_CONNECTED', 'CONNECTED', 'DEGRADED')` | Referenced by `market_candles` and `market_data_status`. | Unique index on `provider_code`. Permanent retention. |
| **10** | `market_candles` | **TimescaleDB Hypertable** (Partitioned by `timestamp`) | **Composite PK: `(symbol_id, timeframe, timestamp)`**; Columns: `symbol_id (UUID FK)`, `timeframe (ENUM: '1M','5M','15M','30M','1H','4H','1D','1W','1MO')`, `timestamp (TIMESTAMPTZ NOT NULL)`, `close_timestamp (TIMESTAMPTZ NOT NULL)`, `open (NUMERIC(18,8))`, `high (NUMERIC(18,8))`, `low (NUMERIC(18,8))`, `close (NUMERIC(18,8))`, `volume (NUMERIC(24,8) NULL)`, `volume_type (ENUM: 'EXCHANGE_VOLUME','TICK_VOLUME','UNAVAILABLE')`, `is_confirmed (BOOL)`, `provider_id (UUID FK)`, `ingested_at (TIMESTAMPTZ)` | `create_hypertable('market_candles', 'timestamp', chunk_time_interval => INTERVAL '7 days')`. Partition column `timestamp` is part of the Composite PK `(symbol_id, timeframe, timestamp)`. `CHECK (high >= low AND high >= open AND high >= close AND low <= open AND low <= close AND close_timestamp > timestamp)`. | Composite PK index `(symbol_id, timeframe, timestamp DESC)`. Columnar compression enabled after 30 days (`segmentby = 'symbol_id, timeframe'`, `orderby = 'timestamp DESC'`); retained permanently. |
| **11** | `market_data_status` | Regular PostgreSQL Table | `id (UUID PK)`, `symbol_id (UUID FK)`, `timeframe (ENUM)`, `provider_id (UUID FK)`, `status ('HEALTHY', 'DATA_UNAVAILABLE', 'NOT_CONNECTED', 'STALE', 'MARKET_CLOSED', 'GAP_DETECTED')`, `last_confirmed_timestamp`, `latency_ms`, `missing_bars_count`, `updated_at` | Unique constraint on `(symbol_id, timeframe)`. Drives Gate 1 of Decision Engine and UI status badges. | Index on `(symbol_id, timeframe, status)`. Live state table + history log. |
| **12** | `system_settings` | Regular PostgreSQL Table | `key (VARCHAR PK)`, `value_json (JSONB)`, `category`, `is_founder_locked (BOOL)`, `updated_by (UUID FK)`, `updated_at` | Stores global & timeframe-specific configurations. Modifying rows with `is_founder_locked = TRUE` requires valid `founder_approvals` record. | PK on `key`, index on `category`. Permanent retention. |
| **13** | `notifications` | Regular PostgreSQL Table | `id (UUID PK)`, `user_id (UUID FK)`, `channel ('IN_APP', 'WEBHOOK', 'EMAIL')`, `severity`, `title`, `payload_json`, `is_read`, `created_at` | FK to `users(id)`. | Index on `(user_id, is_read, created_at DESC)`. Retained 180 days. |
| **14** | `audit_logs` | Regular PostgreSQL Table (Append-Only) | `id (UUIDv7 PK)`, `actor_user_id (UUID FK)`, `actor_role`, `action_type`, `target_entity`, `target_id`, `before_state (JSONB)`, `after_state (JSONB)`, `ip_address`, `created_at (TIMESTAMPTZ)` | **Append-Only Immutable Table** (database trigger blocks `UPDATE` and `DELETE`). Logs all config edits, logins, emergency stops, and approvals. | Index on `(actor_user_id, created_at DESC)` and `(target_entity, target_id)`. Retained minimum 7 years. |
| **15** | `system_logs` | **TimescaleDB Hypertable** (Partitioned by `created_at`) | **Composite PK: `(created_at, id)`**; Columns: `created_at (TIMESTAMPTZ NOT NULL)`, `id (UUIDv7 NOT NULL)`, `service_name`, `level ('DEBUG','INFO','WARN','ERROR','CRITICAL')`, `event_code`, `message`, `context_json (JSONB)` | `create_hypertable('system_logs', 'created_at', chunk_time_interval => INTERVAL '7 days')`. Partition column `created_at` is the leading column of the Composite PK `(created_at, id)` to satisfy TimescaleDB unique-index rules. | Index on `(level, service_name, created_at DESC)`. TimescaleDB retention policy drops chunks older than 90 days (errors exported/retained 1 year). |
| **16** | `api_logs` | **TimescaleDB Hypertable** (Partitioned by `created_at`) | **Composite PK: `(created_at, id)`**; Columns: `created_at (TIMESTAMPTZ NOT NULL)`, `id (UUIDv7 NOT NULL)`, `request_id`, `method`, `path`, `user_id (UUID NULL)`, `status_code (INT)`, `latency_ms (NUMERIC(10,2))`, `ip_address` | `create_hypertable('api_logs', 'created_at', chunk_time_interval => INTERVAL '7 days')`. Partition column `created_at` is the leading column of the Composite PK `(created_at, id)` to satisfy TimescaleDB unique-index rules. | Index on `(path, status_code, created_at DESC)`. TimescaleDB retention policy drops chunks older than 90 days. |
| **17** | `founder_approvals` | Regular PostgreSQL Table | `id (UUID PK)`, `phase_id (UUID FK)`, `approval_type ('PHASE_GATE', 'CONFIG_UNLOCK', 'STRATEGY_PROMOTION', 'PUBLIC_RELEASE')`, `status ('PENDING_FOUNDER_DECISION', 'APPROVED', 'REJECTED')`, `evidence_summary`, `founder_notes`, `decided_by (UUID FK)`, `decided_at` | FK to `project_phases` and `users` (must hold `FOUNDER` role). | Index on `(phase_id, status)`. Permanent immutable governance record. |
| **18** | `project_phases` | Regular PostgreSQL Table | `id (UUID PK)`, `phase_number (INT UNIQUE: 0..9)`, `name`, `status ('PLANNED','DESIGNED','APPROVED','IMPLEMENTED','TESTED','VERIFIED','NOT_IMPLEMENTED','NOT_VERIFIED','BLOCKED','PENDING_FOUNDER_DECISION')`, `updated_at` | Referenced by `founder_approvals`. Tracks official phase progression. | Unique index on `phase_number`. Permanent retention. |
| **19** | `strategy_versions` | Regular PostgreSQL Table | `id (UUID PK)`, `version_tag (VARCHAR NOT NULL)`, `symbol_id (UUID FK)`, `timeframe (ENUM)`, `parameters_json (JSONB)`, `voting_rules_json (JSONB)`, `is_active (BOOL)`, `approved_by_founder_id (UUID FK)`, `created_at` | Immutable snapshot of parameters once activated; ensures every historical signal can reproduce its exact logic version. | Unique index on `(version_tag, symbol_id, timeframe)`. Permanent retention. |
| **20** | `feature_flags` | Regular PostgreSQL Table | `flag_key (VARCHAR PK)`, `is_enabled (BOOL)`, `allowed_roles (TEXT[])`, `requires_founder_approval (BOOL)`, `description`, `updated_at` | Controls private vs. public access, Mode A/B toggles, and future broker adapters. | PK on `flag_key`. Permanent retention. |

#### B. Future Intelligence, Signal, Risk, and Backtesting Entities (Phases 1–8 — 11 Regular PostgreSQL Tables)

| # | Table Name | Table Type | Primary Key & Key Columns | Relationships & Constraints | Indexes & Retention Policy |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **21** | `brain_analyses` | Regular PostgreSQL Table | `id (UUIDv7 PK)`, `symbol_id (UUID FK)`, `timeframe (ENUM)`, `signal_mode ('INDEPENDENT_TIMEFRAME','MTF_CONFIRMED')`, `candle_timestamp (TIMESTAMPTZ)`, `strategy_version_id (UUID FK)`, `active_voters_pool (INT)`, `buy_votes_count (INT)`, `sell_votes_count (INT)`, `neutral_votes_count (INT)`, `abstain_votes_count (INT)`, `aggregate_confidence (NUMERIC(5,2))`, `created_at` | Regular relational table so `id (UUIDv7 PK)` can be referenced by foreign keys in `brain_votes` and `signals`. Unique constraint on `(symbol_id, timeframe, signal_mode, candle_timestamp, strategy_version_id)`. | Composite B-Tree index `(symbol_id, timeframe, candle_timestamp DESC)`. Permanent retention. |
| **22** | `brain_votes` | Regular PostgreSQL Table | `id (UUIDv7 PK)`, `brain_analysis_id (UUID FK)`, `brain_number (INT 1..12)`, `brain_code`, `vote ('BUY','SELL','NEUTRAL','ABSTAIN_DATA_UNAVAILABLE')`, `confidence (NUMERIC(5,2))`, `metrics_json (JSONB)`, `explanation (TEXT)`, `evaluated_at` | FK to `brain_analyses(id) ON DELETE CASCADE`. `CHECK (brain_number BETWEEN 1 AND 12 AND confidence BETWEEN 0 AND 100)`. Unique on `(brain_analysis_id, brain_number)`. | Index on `(brain_analysis_id, brain_number)` and `(brain_code, vote)`. Permanent retention. |
| **23** | `smc_analyses` | Regular PostgreSQL Table | `id (UUIDv7 PK)`, `symbol_id (UUID FK)`, `timeframe (ENUM)`, `candle_timestamp (TIMESTAMPTZ)`, `external_structure`, `internal_structure`, `dealing_range_low`, `dealing_range_high`, `premium_discount_pct`, `active_pois_json (JSONB)`, `liquidity_pools_json (JSONB)`, `sweeps_json (JSONB)`, `smc_status_summary_json (JSONB)`, `created_at` | Captures full Phase 2 SMC snapshot (all 26 features + unified liquidity & OB lifecycle states) at the confirmed candle close. Unique on `(symbol_id, timeframe, candle_timestamp)`. | Index on `(symbol_id, timeframe, candle_timestamp DESC)`. Permanent retention. |
| **24** | `mtf_analyses` | Regular PostgreSQL Table | `id (UUIDv7 PK)`, `symbol_id (UUID FK)`, `execution_timeframe (ENUM)`, `candle_timestamp (TIMESTAMPTZ)`, `htf1_timeframe (ENUM NULL)`, `htf1_closed_timestamp (TIMESTAMPTZ NULL)`, `htf2_timeframe (ENUM NULL)`, `htf2_closed_timestamp (TIMESTAMPTZ NULL)`, `alignment_matrix_json (JSONB)`, `has_conflict (BOOL)`, `conflict_reason`, `created_at` | Enforces `CHECK ((htf1_closed_timestamp IS NULL OR htf1_closed_timestamp <= candle_timestamp) AND (htf2_closed_timestamp IS NULL OR htf2_closed_timestamp <= candle_timestamp))` at the database level to prevent lookahead bias and support `1W`/`1MO` null HTFs. | Index on `(symbol_id, execution_timeframe, candle_timestamp DESC)`. Permanent retention. |
| **25** | `signals` | Regular PostgreSQL Table | `id (UUIDv7 PK)`, `symbol_id (UUID FK)`, `symbol (VARCHAR: 'XAUUSD','BTCUSD')`, `execution_timeframe (ENUM)`, `signal_type ('INDEPENDENT_TIMEFRAME','MTF_CONFIRMED')`, `direction ('BUY','SELL','WAIT')`, `candle_timestamp (TIMESTAMPTZ)`, `brain_analysis_id (UUID FK)`, `smc_analysis_id (UUID FK)`, `mtf_analysis_id (UUID FK NULL)`, `strategy_version_id (UUID FK)`, `strategy_version (VARCHAR)`, `brain_votes_json (JSONB)`, `confidence (NUMERIC(5,2))`, `quality_grade ('A+','A','B','WAIT')`, `mtf_status_json (JSONB)`, `smc_status_json (JSONB)`, `entry_json (JSONB NULL)`, `sl (NUMERIC(18,8) NULL)`, `tp_levels_json (JSONB NULL)`, `invalidation_json (JSONB NULL)`, `explanation (TEXT)`, `signal_status (ENUM)`, `created_at (TIMESTAMPTZ)` | Master Phase 4 record storing and linking all **18 mandatory signal attributes** (Section 14.3). Enforces `CHECK ((direction = 'WAIT' AND quality_grade = 'WAIT' AND entry_json IS NULL AND sl IS NULL AND tp_levels_json IS NULL) OR (direction IN ('BUY','SELL') AND quality_grade IN ('A+','A','B') AND entry_json IS NOT NULL AND sl IS NOT NULL AND tp_levels_json IS NOT NULL))`. | Composite index `(symbol_id, execution_timeframe, signal_type, candle_timestamp DESC)` and index on `(direction, quality_grade, signal_status)`. Permanent retention. |
| **26** | `signal_history` | Regular PostgreSQL Table (Append-Only) | `id (UUIDv7 PK)`, `signal_id (UUID FK)`, `previous_status`, `new_status`, `trigger_price`, `trigger_candle_timestamp`, `notes`, `recorded_at` | FK to `signals(id)`. Tracks every state transition (`CONFIRMED_ACTIVE` $\rightarrow$ `TP1_HIT` $\rightarrow$ `BREAKEVEN_LOCKED` $\rightarrow$ `TP2_HIT` or `SL_HIT`/`INVALIDATED`/`EXPIRED`). | Index on `(signal_id, recorded_at ASC)`. Permanent audit retention. |
| **27** | `trade_plans` | Regular PostgreSQL Table | `id (UUID PK)`, `signal_id (UUID UNIQUE FK)`, `entry_style ('SNIPER','FAST_SCALPER')`, `entry_price`, `entry_zone_low`, `entry_zone_high`, `stop_loss`, `tp1_price`, `tp2_price`, `tp3_price`, `rr_tp1`, `rr_tp2`, `rr_tp3`, `tp1_close_pct`, `tp2_close_pct`, `tp3_close_pct`, `invalidation_price`, `invalidation_rule`, `expires_at` | 1-to-1 relational breakdown of `entry_json`, `sl`, `tp_levels_json`, and `invalidation_json` for actionable `BUY` and `SELL` signals (`CHECK (entry_price != stop_loss)`). | Unique index on `signal_id`. Permanent retention. |
| **28** | `risk_records` | Regular PostgreSQL Table | `id (UUIDv7 PK)`, `trade_plan_id (UUID FK)`, `account_equity_ref`, `risk_pct`, `calculated_position_units`, `spread_at_eval`, `daily_drawdown_pct`, `max_drawdown_pct`, `consecutive_losses_count`, `risk_gate_passed (BOOL)`, `veto_reason`, `created_at` | FK to `trade_plans(id)`. Logs Phase 5 risk sizing and portfolio circuit-breaker checks. | Index on `(trade_plan_id)` and `(risk_gate_passed, created_at DESC)`. Permanent retention. |
| **29** | `news_events` | Regular PostgreSQL Table | `id (UUID PK)`, `event_code`, `title`, `currency_or_asset ('USD','XAU','BTC')`, `impact_level ('HIGH','MEDIUM','LOW')`, `scheduled_at (TIMESTAMPTZ)`, `previous_val`, `forecast_val`, `actual_val`, `source_name`, `source_reliability_score`, `protection_window_start`, `protection_window_end`, `ingested_at` | Drives Phase 6 News Intelligence and Gate 2 Market Protection freezes. | Index on `(scheduled_at, impact_level, currency_or_asset)` and `(protection_window_start, protection_window_end)`. Permanent retention for historical backtesting. |
| **30** | `backtest_runs` | Regular PostgreSQL Table | `id (UUID PK)`, `strategy_version_id (UUID FK)`, `symbol_id (UUID FK)`, `timeframe (ENUM)`, `signal_type (ENUM)`, `run_type ('IN_SAMPLE','OUT_OF_SAMPLE','WALK_FORWARD','PAPER_FORWARD')`, `start_timestamp`, `end_timestamp`, `spread_model_json`, `slippage_model_json`, `status`, `executed_by (UUID FK)`, `created_at` | Tracks Phase 8 historical test configurations per market, timeframe, and mode. | Index on `(symbol_id, timeframe, strategy_version_id, run_type)`. Permanent retention. |
| **31** | `performance_metrics` | Regular PostgreSQL Table | `id (UUID PK)`, `backtest_run_id (UUID UNIQUE FK)`, `total_trades`, `win_rate_pct`, `profit_factor`, `expectancy_r`, `average_r`, `max_drawdown_pct`, `recovery_factor`, `avg_trade_duration_sec`, `tp1_hit_rate_pct`, `tp2_hit_rate_pct`, `tp3_hit_rate_pct`, `sl_hit_rate_pct`, `max_consecutive_losses`, `regime_breakdown_json`, `session_breakdown_json` | 1-to-1 summary table for `backtest_runs`. Never stores fabricated metrics; populated exclusively by completed engine runs. | Unique index on `backtest_run_id`. Permanent retention. |

---

## 23. API Architecture & Cross-Boundary Schema Synchronization

### 23.1 REST & WebSocket API Design Principles & Unified 18-Field Signal Contract
- **Versioned Prefix:** All endpoints are versioned under `/api/v1/...`.
- **Standardized Envelope:** Every JSON response includes `{ "status": "success" | "error", "data": ..., "meta": { "timestamp_utc": "...", "symbol": "...", "timeframe": "...", "data_status": "HEALTHY" | "DATA_UNAVAILABLE" | "NOT_CONNECTED" | "MARKET_CLOSED" | "STALE" }, "error": null | { "code": "...", "message": "..." } }`.
- **Strict Timeframe Validation Middleware:** All routes accepting `:timeframe` validate against the canonical internal enum `{'1M','5M','15M','30M','1H','4H','1D','1W','1MO'}`. Any TradingView webhook payload containing a Pine Script timeframe string (`"1"`, `"60"`, `"240"`, `"1M"`) is translated through the Section 6.2 adapter (`f_pine_to_quantum_tf`) and validated against an explicit `timeframe_namespace: "QUANTUM_INTERNAL" | "PINE_SCRIPT_V6"` field so `"1M"` (1 Minute internal vs. 1 Month Pine) can never be misrouted.
- **Cross-Layer 18-Field `SignalRecord` Contract Parity (Section 14.3 $\leftrightarrow$ Section 22.3 `signals` Table $\leftrightarrow$ REST/WS API $\leftrightarrow$ Pine Webhook $\leftrightarrow$ TypeScript Frontend):**
  - Every layer serializes and validates the exact same 18 canonical field names defined in Section 14.3:
    `signal_id` (mapped to `signals.id`), `symbol`, `execution_timeframe`, `signal_type`, `direction`, `candle_timestamp`, `brain_votes` (mapped to `signals.brain_votes_json` & `brain_votes` rows), `confidence`, `quality_grade`, `mtf_status` (`signals.mtf_status_json`), `smc_status` (`signals.smc_status_json`), `entry` (`signals.entry_json` & `trade_plans`), `sl` (`signals.sl` & `trade_plans.stop_loss`), `tp_levels` (`signals.tp_levels_json` & `trade_plans.tp1..3`), `invalidation` (`signals.invalidation_json` & `trade_plans.invalidation_*`), `explanation`, `strategy_version`, and `signal_status`.

### 23.2 Core API Endpoint Catalog

| Domain | Method & Path | Purpose & RBAC Requirement |
| :--- | :--- | :--- |
| **Auth & Sessions** | `POST /api/v1/auth/login`<br>`POST /api/v1/auth/logout`<br>`POST /api/v1/auth/mfa/verify`<br>`GET /api/v1/auth/me` | Authenticate user credentials, verify TOTP MFA, manage HttpOnly secure session cookies, and return active role permissions. |
| **Market Data & Status** | `GET /api/v1/markets/:symbol/candles?timeframe=15M&limit=500`<br>`GET /api/v1/markets/status` | Retrieve confirmed OHLCV candles for any of the 9 timeframes and inspect live provider connection/latency status (`HEALTHY`, `DATA_UNAVAILABLE`, `NOT_CONNECTED`, `MARKET_CLOSED`, `STALE`). |
| **12-Brain Intelligence** | `GET /api/v1/intelligence/:symbol/:timeframe/brains?mode=MTF_CONFIRMED` | Return the latest confirmed 12-Brain vote tally, individual brain votes (`BUY`/`SELL`/`NEUTRAL`/`ABSTAIN_DATA_UNAVAILABLE`), confidence scores, and explanations. |
| **SMC & MTF State** | `GET /api/v1/intelligence/:symbol/:timeframe/smc`<br>`GET /api/v1/intelligence/:symbol/:timeframe/mtf` | Return active Order Blocks (with 6-state lifecycle), Breaker/Mitigation Blocks, FVGs, Liquidity Pools (with 7-state lifecycle), Dealing Range Premium/Discount %, and 9-timeframe MTF alignment matrix. |
| **Master Decisions & Signals** | `GET /api/v1/signals/:symbol/:timeframe/latest?mode=MTF_CONFIRMED`<br>`GET /api/v1/signals/history?symbol=XAUUSD&timeframe=1H&mode=...`<br>`GET /api/v1/signals/:signal_id` | Fetch latest confirmed Master Decision (`BUY`/`SELL`/`WAIT`), complete 18-field `SignalRecord` JSON payload, `trade_plans` (`Entry`, `SL`, `TP1/2/3`), and filtered historical ledger. |
| **Risk & Protection** | `POST /api/v1/risk/calculate-position`<br>`GET /api/v1/protection/status`<br>`GET /api/v1/news/calendar` | Compute position size for given equity/SL, check spread/volatility/news protection circuit-breaker state (including fail-closed `NEWS_DATA_UNAVAILABLE`), and view economic calendar countdowns. |
| **Backtesting & Analytics** | `POST /api/v1/backtests/run`<br>`GET /api/v1/backtests/:run_id/metrics`<br>`GET /api/v1/analytics/:symbol/:timeframe` | Launch historical/walk-forward backtests (`Founder`, `Admin`, `Private Tester`) and retrieve verified performance metrics per market & timeframe. |
| **TradingView Webhook** | `POST /api/v1/webhooks/tradingview` | Authenticated endpoint validating body `webhook_secret` via constant-time `hmac.compare_digest`, Redis `event_nonce` replay protection, timestamp freshness (`<= 60s`), rate limit, optional IP allowlist, and backend candle cross-verification. |
| **Admin & Founder Governance** | `POST /api/v1/founder/phases/:phase_num/approve`<br>`POST /api/v1/founder/emergency-stop`<br>`PUT /api/v1/founder/settings/:key`<br>`GET /api/v1/admin/audit-logs` | **Founder-Only** endpoints for phase gate approval, locked config updates, and system-wide Emergency Stop; Admin endpoints for audit log and user review. |
| **Real-Time WebSocket** | `WSS /api/v1/ws/stream` | Authenticated WebSocket multiplexing channels: `candle.confirmed.{symbol}.{tf}`, `decision.emitted.{symbol}.{tf}`, and `protection.alert.{symbol}`. |

---

## 24. Security Architecture & Threat Model

### 24.1 Comprehensive Security Controls Matrix (24 Mandatory Controls)

| # | Security Control | Implementation Specification in QUANTUM |
| :--- | :--- | :--- |
| **1** | **Authentication** | Multi-layered authentication with short-lived access tokens (`15 min`) and rotating refresh sessions bound to device fingerprint and IP metadata. Invite-only account creation during Private phase. |
| **2** | **Password Hashing** | **Argon2id** (`memory_cost=65536 KiB`, `time_cost=3`, `parallelism=4`) with unique per-user cryptographic salt. Minimum password policy: 12+ characters with entropy check against breached password lists. |
| **3** | **Email Verification** | Time-bound (`30 min`), single-use cryptographically random SHA-256 hashed verification tokens required before account activation. |
| **4** | **Password Reset** | Constant-time response endpoint issuing single-use, 15-minute expiring reset tokens; automatically revokes all active sessions upon password change. |
| **5** | **Session Management** | Server-side revocable session store (`sessions` table + Redis cache); immediate session invalidation on logout, role downgrade, or suspicious IP jump. |
| **6** | **Role-Based Access Control (RBAC)** | Deny-by-default middleware checking both `role_code` and fine-grained `permission_code` on every REST endpoint and WebSocket subscription. |
| **7** | **Optional / Role-Enforced MFA** | Time-Based One-Time Password (**TOTP**, RFC 6238) with encrypted secrets at rest (`AES-256-GCM`). **Mandatory for `FOUNDER` and `ADMIN` roles**; optional/recommended for all other roles. |
| **8** | **Rate Limiting** | Redis-backed sliding-window rate limiter per IP and per User ID (e.g., Auth routes: `5 req/min`; Webhook ingress: `30 req/min`; Standard API: `120 req/min`; Heavy Backtest trigger: `5 req/hour`). |
| **9** | **Input Validation** | Strict schema validation via Pydantic v2 (Backend) and Zod/TypeScript (Frontend) rejecting unexpected fields (`extra='forbid'`), invalid symbols, or ambiguous timeframe strings. |
| **10** | **SQL Injection Protection** | 100% parameterized queries via SQLAlchemy 2.0 ORM; raw string concatenation into SQL queries is strictly prohibited by static linter rules (`bandit` / `ruff`). |
| **11** | **XSS Protection** | React automatic output encoding, strict Content-Security-Policy (`CSP`) headers disallowing `unsafe-inline` scripts, and DOM sanitization on any external news text. |
| **12** | **CSRF Protection** | Double-submit cryptographic CSRF tokens paired with `SameSite=Strict` cookies on all state-mutating cookie-authenticated requests. |
| **13** | **Secure Cookies** | `HttpOnly; Secure; SameSite=Strict; Path=/` attributes enforced on session cookies. |
| **14** | **HTTPS / TLS** | TLS 1.3 enforced for all external traffic (`HTTPS` and `WSS`) with HSTS preload header (`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`). |
| **15** | **CORS Policy** | Strict allowlist restricting origins exclusively to the official QUANTUM frontend domain; wildcard `*` origins with credentials are forbidden. |
| **16** | **API Authentication** | Bearer JWT / Session signature verification + scoped service tokens for internal worker communication. |
| **17** | **Webhook Authentication (TradingView Inbound & Backend Outbound)** | **Realistic TradingView Platform Constraint & 6-Layer Inbound Security:** TradingView's native webhook dispatcher sends a standard `POST` request and **cannot** attach custom HTTP authentication headers or compute dynamic `HMAC-SHA256` signatures over arbitrary JSON request bodies inside TradingView's cloud server. Therefore, `/api/v1/webhooks/tradingview` implements a 6-layer defense-in-depth verification pipeline:<br>1. **TLS 1.3 HTTPS Transport:** Protects the JSON body in transit.<br>2. **Cryptographic Body Secret (`webhook_secret`):** 256-bit (64-hex-char) high-entropy secret embedded inside the Pine Script JSON alert payload (`"webhook_secret": "..."`), validated on the backend via constant-time `hmac.compare_digest(hashlib.sha256(provided_secret).digest(), stored_secret_sha256)` so raw secrets are never exposed to timing attacks.<br>3. **Timestamp Freshness Window:** Asserts `abs(server_now_utc - payload.alert_dispatched_at_utc) <= 60 seconds` and `payload.candle_close_timestamp <= server_now_utc + 5s`.<br>4. **Deterministic Nonce Replay Protection:** Computes `event_nonce = f"{symbol}:{execution_timeframe}:{candle_timestamp}:{signal_type}:{direction}"` and executes atomic Redis `SET event_nonce "1" NX EX 86400`; duplicate/replayed payloads are rejected with `409 Conflict`.<br>5. **Configurable Egress IP Allowlist (Defense-in-Depth Only):** Optionally checks source IP against TradingView's documented webhook egress IPs (`52.89.214.238`, `34.212.75.30`, `54.218.53.128`, `52.32.178.7`), configurable via `system_settings` in case TradingView rotates cloud IPs, and **never** relied upon as the sole authentication mechanism.<br>6. **Backend-Authoritative Market State Cross-Verification:** Incoming TradingView webhooks are treated as **advisory telemetry/triggers**, never blind execution orders—the backend cross-verifies the reported `close`, `candle_timestamp`, and Phase 6 News Protection status against its own primary market data feed before recording or broadcasting any signal.<br>*(Note: For **Outbound Webhooks** sent FROM the QUANTUM backend to external subscriber endpoints, the backend DOES compute and attach an `X-Quantum-Signature-256: sha256=<HMAC_SHA256(secret, raw_body)>` HTTP header).* |
| **18** | **Secret Management** | Zero hardcoded credentials or API keys in source code or Docker images. All secrets injected at runtime via environment variables / cloud secret manager, verified by pre-commit secret scanning (`gitleaks`). |
| **19** | **Database Permissions** | Principle of Least Privilege: Application runtime uses a restricted DB role (`quantum_app_role`) without `DROP TABLE` or `TRUNCATE` privileges; `audit_logs` and `signal_history` grant `INSERT, SELECT` only (no `UPDATE` or `DELETE`). |
| **20** | **Audit Logging** | Immutable append-only `audit_logs` recording actor, role, IP, timestamp, and before/after JSON diff for all privileged operations. |
| **21** | **Encrypted Backups** | Automated database backups encrypted at rest using `AES-256-GCM` with off-site key separation. |
| **22** | **Dependency Scanning** | Automated vulnerability scanning in CI pipeline (`pip-audit`, `npm audit`, Trivy container scan) blocking builds on critical CVEs. |
| **23** | **Security Headers** | Enforces `Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, `Referrer-Policy: strict-origin-when-cross-origin`, and `Permissions-Policy`. |
| **24** | **Abuse & Bot Protection** | Automated IP lockouts on repeated auth/webhook failures, anomaly detection on API scraping attempts, and WebSocket connection quotas per user. |

### 24.2 System Threat Model (STRIDE Analysis)

| Threat Category | Specific Attack Scenario | Impact Severity | Engineered Mitigation in QUANTUM |
| :--- | :--- | :--- | :--- |
| **Spoofing** | Attacker sends forged or replayed HTTP POST requests to `/api/v1/webhooks/tradingview` attempting to inject fake `BUY`/`SELL` signals. | Critical | 6-layer verification: TLS 1.3 + 256-bit `webhook_secret` constant-time digest check + 60s timestamp freshness + Redis `SET NX` `event_nonce` replay rejection + optional IP allowlist + backend authoritative candle & Phase 6 News Protection cross-verification. |
| **Tampering** | Malicious or compromised Admin attempts to modify historical signal outcomes, delete audit logs, or alter Founder-locked configuration settings. | Critical | Database-level trigger blocks `UPDATE`/`DELETE` on `audit_logs` and `signal_history`; `system_settings` rows with `is_founder_locked = TRUE` reject mutations without a cryptographic `FOUNDER` role signature. |
| **Repudiation** | Disputed parameter change in Strategy Lab alters live signal thresholds without accountability. | High | Every configuration change creates an immutable `strategy_versions` snapshot and an `audit_logs` entry linking `actor_user_id`, IP, and exact JSON diff. |
| **Information Disclosure** | Unauthorized user attempts to access Private Beta endpoints, proprietary 12-Brain strategy weights, or leaked API keys in client bundle. | High | All 12-Brain calculations and provider API keys reside strictly on the backend server; client bundles contain zero provider keys (`VITE_` / `NEXT_PUBLIC_` restricted to non-sensitive public config). |
| **Denial of Service (DoS)** | Flood of concurrent 9-timeframe historical backtest requests starves CPU from the real-time `1M`/`5M` signal evaluation loop. | High | Complete process isolation: real-time candle ingestion and live signal evaluation run on dedicated high-priority Celery queues/workers, separate from rate-limited background backtest workers. |
| **Elevation of Privilege** | Admin or Private Tester attempts to invoke `/api/v1/founder/*` routes to approve a phase or enable public registration. | Critical | Dedicated RBAC guard explicitly verifying `role == 'FOUNDER'` + active TOTP MFA session; Admins are explicitly denied access to Founder controls. |

---

## 25. Market Data Architecture & Provider Evaluation

### 25.1 Strict Data Integrity & Anti-Fabrication Rules
1. **Zero Data Fabrication:** QUANTUM must **never** generate random, synthetic, or interpolated prices to mask a missing live feed.
2. **Standardized Status Labels:**
   - When required market or news data cannot be fetched or fails validation: **`DATA UNAVAILABLE`**.
   - When a data provider adapter is unconfigured or disconnected: **`NOT CONNECTED`**.
   - When the exchange/OTC session for a market is legitimately closed (e.g., `XAUUSD` weekend or daily 60-minute rollover): **`MARKET_CLOSED`**.
   - When an active market misses its expected confirmed candle beyond the grace window: **`STALE`** or **`GAP_DETECTED`**.
   - If historical sample/demo fixtures are loaded in a local development or unit-test sandbox, the UI must render a persistent high-contrast watermark badge: **`DEMO / HISTORICAL FIXTURE DATA — NOT LIVE`**.

### 25.2 Market Data Technical Requirements, DST Session Boundaries & Calendar-Aware Gap Detection
- **Nine-Timeframe Coverage (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`):**
  - Providers supply native OHLCV endpoints for standard intervals or tick/1M streams from which higher timeframes are deterministically aggregated and cross-checked against provider native HTF candles.
- **Authoritative Timezone & Candle Boundary Normalization:**
  - All internal timestamps are stored and indexed strictly in **UTC (`TIMESTAMPTZ`)**, while session boundaries and daily/weekly closes for `XAUUSD` are computed dynamically via the **IANA `America/New_York` timezone database (`zoneinfo.ZoneInfo("America/New_York")`)** in complete synchronization with Section 5.2 and Section 6.4:
    - **Sub-Hourly & Hourly Candles (`1M`, `5M`, `15M`, `30M`, `1H`):** Align cleanly to standard UTC minute/hour boundaries.
    - **4-Hour Candles (`4H`):** Follow the authoritative `four_hour_alignment_mode` in Section 6.4 (`UTC_MODULO_4H` opening at `00:00, 04:00, 08:00, 12:00, 16:00, 20:00 UTC` by default, or `NY_SESSION_4H` aligned to `17:00 America/New_York`).
    - **Daily (`1D`) & Weekly (`1W`) Candles:**
      - `BTCUSD`: Daily candles open/close at **`00:00:00 UTC`** (exact `86,400s` per day, `604,800s` per 7-day week, 24/7/365).
      - `XAUUSD`: Daily candles close at **`17:00:00 America/New_York`** (and reopen at `18:00:00 America/New_York` after the 60-minute daily CME/Globex maintenance rollover), which equals **`21:00 UTC` during US Daylight Saving Time (EDT, `UTC-4`)** and **`22:00 UTC` during US Standard Time (EST, `UTC-5`)**. Weekly `XAUUSD` candles open Sunday `18:00 America/New_York` and close Friday `17:00 America/New_York`. *(Or `00:00 UTC` if configured by Founder under `PFD-06`).*
    - **Monthly (`1MO`) Candles:** Align strictly to calendar month boundaries (`1st day of calendar month at 00:00:00 UTC` to the first instant of the next calendar month `00:00:00 UTC`, or the first trading session open/last trading session close of the calendar month for `XAUUSD`).
- **Calendar-Aware & Session-Aware Gap Detection Algorithm (Fixing Fixed-Second `1MO` & DST Bugs):**
  - **Root Cause of Fixed-Second Bug:** A fixed constant `timeframe_seconds` (such as `2,592,000s = 30 days`) **cannot** be used to detect gaps on `1MO` (Monthly) candles—nor on `XAUUSD` `1D` candles across a US DST transition weekend—because calendar months have variable lengths (`28`, `29`, `30`, or `31` days):
    - **February (Non-Leap Year):** $28 \text{ days} = 2,419,200 \text{ seconds}$ (would fail a `< 30-day` check or miss a gap).
    - **February (Leap Year, where `year % 4 == 0 and (year % 100 != 0 or year % 400 == 0)`):** $29 \text{ days} = 2,505,600 \text{ seconds}$.
    - **30-Day Months (`Apr, Jun, Sep, Nov`):** $30 \text{ days} = 2,592,000 \text{ seconds}$.
    - **31-Day Months (`Jan, Mar, May, Jul, Aug, Oct, Dec`):** $31 \text{ days} = 2,678,400 \text{ seconds}$ (would trigger a false-positive `GAP_DETECTED` if compared against `2,592,000s`!).
  - **Deterministic Next-Expected-Timestamp Function (`compute_next_expected_open_utc`):**
    1. **For Fixed-Duration Timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, and `BTCUSD` `1D`/`1W`):**
       $$\text{expected\_next\_open}(t_{\text{prev}}) = t_{\text{prev}} + \Delta t_{\text{fixed}}$$
       where for `XAUUSD`, if $t_{\text{prev}} + \Delta t_{\text{fixed}}$ falls inside the daily rollover break (`17:00–18:00 America/New_York`), the weekend closure (`Friday 17:00 America/New_York` to `Sunday 18:00 America/New_York`), or an exchange holiday in `market_holiday_calendar`, the function advances to the exact next active session open (`Sunday 18:00 America/New_York` or `18:00 America/New_York` post-rollover).
    2. **For `XAUUSD` Daily (`1D`) & Weekly (`1W`) Candles Across DST Transitions:**
       - Converts $t_{\text{prev}}$ to `ZoneInfo("America/New_York")`, adds `relativedelta(days=+1)` (skipping Friday-to-Sunday weekend closures and exchange holidays), anchors to `18:00:00 America/New_York` (session open) / `17:00:00 America/New_York` (session close), and converts back to `UTC`. This handles the 23-hour spring-forward DST day and 25-hour fall-back DST day with zero false gap alerts.
    3. **For Monthly (`1MO`) Candles (Calendar-Aware Arithmetic):**
       - Computes expected candle close and next candle open using exact calendar month arithmetic (`dateutil.relativedelta.relativedelta(months=+1)` or `calendar.monthrange(year, month)`):
         $$\text{days\_in\_month}(Y, M) \in \{28, 29, 30, 31\}$$
         $$\text{expected\_next\_open}_{1\text{MO}}(t_{\text{prev}}) = \text{ FirstCalendarBoundaryOfNextMonth}(t_{\text{prev}} + \text{relativedelta}(\text{months}=+1))$$
         $$\text{expected\_duration\_seconds}_{1\text{MO}}(Y, M) = \text{days\_in\_month}(Y, M) \times 86,400$$
       - A monthly gap (`GAP_DETECTED`) is flagged **if and only if** `t_current > expected_next_open_1MO(t_prev)` (i.e., one or more calendar months `(Y, M)` are missing between $t_{\text{prev}}$ and $t_{\text{current}}$), or if a closed monthly candle's `close_timestamp` does not match the end of that calendar month.
- **Additional Data Quality & Anomaly Pipeline Guards:**
  - **Duplicate Data:** Deduplicates repeated candle payloads via idempotent upsert on composite primary key `(symbol_id, timeframe, timestamp)` while verifying OHLC consistency.
  - **Out-of-Order Timestamps:** Buffers and sorts incoming stream packets; rejects stale out-of-order ticks arriving after a candle has already been sealed as `is_confirmed = TRUE`.
  - **Spike / Bad Tick Filtering:** Flags corrupt provider ticks where high/low deviates by $> 10 \times \text{ATR}(14)$ within a single sub-second tick without matching cross-provider confirmation.

### 25.3 Market Data Provider Evaluation & Adapter Compatibility Matrix

*(Selection of primary and fallback providers is marked `PENDING FOUNDER DECISION` under `PFD-04`.)*

| Provider | Exact Symbol Tickers (`XAUUSD` / `BTCUSD`) | Native 9-Timeframe API Intervals (`1M`–`1MO`) | Historical Depth (`1M` vs. `1MO`) & Volume Type | Quote Currency & Session Alignment Notes | Cost, Licensing & Suitability Assessment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Twelve Data** | `XAU/USD` (Spot Gold OTC)<br>`BTC/USD` (Spot USD Crypto Index) | `1min`, `5min`, `15min`, `30min`, `1h`, `4h`, `1day`, `1week`, `1month` (All 9 native) | `XAU/USD`: 20+ yrs daily/monthly (`>240` `1MO` bars).<br>`BTC/USD`: back to ~2011–2013 (`~155–180` `1MO` bars).<br>Volume: Tick/Aggregated for Gold; Exchange volume for BTC. | True `USD` quote for both `XAU/USD` and `BTC/USD`. Supports `timezone=America/New_York` or `UTC`. | Free dev tier (8 req/min); Paid Pro tiers ($29–$329+/mo). Commercial display license required for Phase 9 public launch. **High Suitability** for unified 9-TF schema. |
| **Polygon.io (Massive)** | `C:XAUUSD` (Forex/Metals)<br>`X:BTCUSD` (Multi-Exchange USD Spot Aggregate) | Custom multiplier aggregates: `1,5,15,30/minute`, `1,4/hour`, `1/day`, `1/week`, `1/month` (All 9 native) | `C:XAUUSD`: 15–20+ yrs.<br>`X:BTCUSD`: 10+ yrs (`~125–145` `1MO` bars).<br>Volume: OTC quote tick count (`v`) for `C:XAUUSD`; true USD exchange volume for `X:BTCUSD`. | True `USD` quote (`X:BTCUSD` aggregates Coinbase, Kraken, Bitstamp, Gemini USD pairs—no USDT basis). UTC timestamps. | Individual plans ($29–$199/mo); Business license required before Phase 9 public redistribution. **High Suitability** for low-latency WebSocket + historical backtesting. |
| **OANDA v20 API** | `XAU_USD` (Institutional Bullion CFD)<br>`BTC_USD` (where supported) | `M1`, `M5`, `M15`, `M30`, `H1`, `H4`, `D`, `W`, `M` (All 9 native) | `XAU_USD`: 20+ yrs (`>240` `1MO` bars back to 2004).<br>Volume: Authentic institutional broker tick volume + real `bid`/`ask` spread candles (`MBA`). | Native `America/New_York` `17:00` daily close alignment (`dailyAlignment=17`, `alignmentTimezone=America/New_York`). | Free with OANDA account for private/internal use; public redistribution prohibited without institutional contract. **Best Reference Feed for `XAUUSD`** in Private Beta. |
| **Coinbase Advanced / Kraken / Bitstamp Direct Spot APIs** | Coinbase: `BTC-USD`<br>Kraken: `XXBTZUSD`<br>Bitstamp: `btcusd` | Native or deterministic `1M`-aggregated candles across `1m..1d` + `1w`/`1MO` rollup | Bitstamp `btcusd`: back to **Aug 2011** (`~183` `1MO` bars).<br>Coinbase `BTC-USD`: back to **2015** (`~135` `1MO` bars).<br>Volume: 100% authentic `BTC` spot trade volume. | True **fiat `USD` orderbooks** (zero `USDT` stablecoin depeg distortion). 24/7 `00:00 UTC` boundaries. | $0 public market data WebSockets/REST. **Recommended Primary/Stitching Source for `BTCUSD`** true spot USD price and volume. |
| **Binance Spot API** | `BTCUSDT` *(Proxy)* or `BTCUSD` *(where active)* | `1m`, `5m`, `15m`, `30m`, `1h`, `4h`, `1d`, `1w`, `1M` (All 9 native) | `BTCUSDT`: back to **Aug 2017** (`~110` `1MO` bars).<br>Volume: Deepest global crypto exchange trade volume. | Quoted in **`USDT` (`BTCUSDT`)**. Per Section 5.3, requires live `USDT/USD` basis guard (`<= 15 bps`) or use strictly as secondary volume/funding telemetry alongside a true `BTC-USD` primary feed. | $0 public streams. **High Suitability as Secondary Liquidity/Volume & Phase 6 Derivatives Feed**, paired with Bitstamp/Coinbase/Polygon for pre-2017 `BTCUSD` history. |

### 25.4 Monthly (`1MO`) Historical Data Depth Analysis & Multi-Provider Historical Stitching
- **Mathematical Reality of `1MO` Historical Bars (`250 Monthly Bars = 20.83 Years`):**
  - While `250` bars on `1M` requires only `4.17 hours` and `250` bars on `1D` requires `~11.5 months`, **`250` confirmed monthly (`1MO`) bars requires `20 years and 10 months` of continuous historical data**.
  - **Impact on `XAUUSD` (Gold):** Spot Gold (`XAUUSD`) has continuous institutional electronic history dating back to the 1970s–2000s (`> 300` monthly candles readily available via OANDA v20, Twelve Data, and LBMA/FRED archives). Thus, `XAUUSD` easily satisfies the full `>= 250` bar standard warm-up even on `1MO`.
  - **Impact on `BTCUSD` (Bitcoin):** Bitcoin's Genesis Block was mined in January 2009, and the first public USD exchange trading (Mt. Gox / NewLibertyStandard / Bitstamp) began in **2010–2011**. As of 2026, **fewer than `200` monthly candles of `BTCUSD` exist in human history** (`~183` monthly bars since Bitstamp's August 2011 launch; `~195` monthly bars since July 2010 early index data), and single-exchange APIs launched later (e.g., Coinbase 2015 = `~135` `1MO` bars; Binance 2017 = `~110` `1MO` bars) have even fewer monthly bars.
- **Engineered Solution (No Silent Rule Weakening):**
  1. **Multi-Provider Historical Stitching for `BTCUSD` (`1D`, `1W`, `1MO`):**
     - During Phase 0 historical backfill, the `ingestion_service` stitches verified early `BTCUSD` daily/monthly spot index history (`2010-07` to `2015-01` from Bitstamp `btcusd` / brave-new-coin / historical spot archive) with primary live exchange history (`2015-01` to present), tagging early pre-exchange-API bars with their exact `provider_id` so `BTCUSD` achieves the maximum historically possible `~183–195` `1MO` candles (and `> 5,500` `1D` candles / `> 800` `1W` candles).
  2. **Explicit `1MO` Macro Warm-Up Scaling Profile (Section 7.2 & Section 11.2 Brain 1):**
     - **Timeframes `1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`:** Strictly enforce the `200`-bar minimum (`EMA 20 / 50 / 200`) and `250`-bar full convergence requirement on **both** `XAUUSD` and `BTCUSD`. No exceptions.
     - **Timeframe `1MO` Only:**
       - If `available_confirmed_bars >= 200` (e.g., `XAUUSD` with 20+ years of monthly data), Brain 1 uses the standard `EMA 20 / 50 / 200` stack.
       - If `60 <= available_confirmed_bars < 200` on `1MO` (e.g., `BTCUSD` where `< 200` monthly bars exist in the entire lifespan of the asset, or a provider returning 5–16 years of monthly data), Brain 1 explicitly activates the **`1MO_MACRO_PROFILE`** (`EMA 12` [1-Year], `EMA 24` [2-Year], `EMA 60` [5-Year] + `ADX(14)` + `ATR(14)`), applying a `0.90x` confidence scaling factor and recording `"warmup_profile": "1MO_MACRO_60_BAR"` in `metrics_json`.
       - If `available_confirmed_bars < 60` on `1MO` (`< 5 years` of monthly data), Brain 1 outputs **`ABSTAIN_DATA_UNAVAILABLE`** and the system displays **`DATA UNAVAILABLE`** on `1MO`.

---

## 26. User Roles & Extensible Permission System

### 26.1 Five-Tier Role Hierarchy & Permission Matrix

| Capability / Permission Scope | 1. Founder / Super Admin | 2. Admin | 3. Private Tester | 4. Free User *(Future Phase 9)* | 5. Premium User *(Future Phase 9)* |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Final Project & Phase Approval (`phase:approve`)** | **YES (Exclusive)** | NO | NO | NO | NO |
| **Modify Locked Project Configurations (`config:locked:write`)** | **YES (Exclusive)** | NO | NO | NO | NO |
| **Promote Strategy Version to Production (`strategy:promote`)** | **YES (Exclusive)** | NO | NO | NO | NO |
| **Enable Public Registration / Paid Tiers (`release:public:toggle`)** | **YES (Exclusive)** | NO | NO | NO | NO |
| **Trigger System-Wide Emergency Stop (`killswitch:global`)** | **YES** | YES (Trigger only; Founder required to unlock) | NO | NO | NO |
| **Manage Users & Private Tester Invitations (`users:manage`)** | **YES** | YES (Cannot modify Founder account) | NO | NO | NO |
| **View System, API, and Security Audit Logs (`logs:audit:read`)** | **YES** | YES (Read-Only) | NO | NO | NO |
| **Access All 9 Timeframes (`1M`–`1MO`) & Both Markets** | **YES** | YES | YES | Restricted (e.g., Delayed or Subset per Founder config) | YES (Full Real-Time 9 Timeframes) |
| **Access 12-Brain, SMC, MTF & Decision Dashboards** | **YES** | YES | YES | Summary View Only | YES (Full Deep-Dive Telemetry) |
| **Run Strategy Lab Backtests & Walk-Forward Tests** | **YES** | YES | YES (Sandboxed) | NO | Configurable by Founder |
| **Submit Structured Bug Reports & Tester Feedback** | **YES** | YES | YES | YES | YES |

### 26.2 Strict Governance Locks
1. **Admin Subordinate Rule:** The `ADMIN` role is strictly operational. An Admin cannot alter `is_founder_locked` settings, cannot modify or demote a `FOUNDER` user, cannot approve development phases, and cannot enable public access.
2. **Private-First Enforcement:** In Phases 0 through 8 (and Phase 9A Private Beta), public self-registration (`/register`) and paid subscription checkouts are disabled via `feature_flags` (`PUBLIC_REGISTRATION_ENABLED = FALSE`, `PAID_SUBSCRIPTIONS_ENABLED = FALSE`). Only accounts provisioned by the Founder or via Founder-authorized single-use invitation tokens can authenticate.

---

## 27. Phase 0–9 Complete Development Roadmap

> **IMPORTANT RESTRICTION:** All phases below are documented as the Master Blueprint specification (`Status: PLANNED / DESIGNED`). **Zero code implementation of Phase 0 through Phase 9 is permitted until the Founder reviews this README.md and issues an explicit phase-specific prompt.**

---

### PHASE 0 — FOUNDATION AND PROJECT ARCHITECTURE
- **Status:** `DESIGNED` (`NOT IMPLEMENTED`)
- **Purpose:** Establish the complete technical foundation, infrastructure scaffolding, database schema (31 tables), RBAC authentication, Founder governance console, and market data ingestion pipelines without implementing trading intelligence.
- **Scope & Deliverables (Reconciliation of the 32 Phase 0 Architectural Documentation Items vs. the 31 Database Tables):**
  - *Note on Numbers (`32` vs. `31`):* The **32 Phase 0 Blueprint Items** represent the 32 architectural and engineering specifications documented across Sections 1–39 of this blueprint, whereas the **31 Database Tables** (20 Phase 0 operational tables + 11 Phase 1–8 intelligence tables defined in Section 22.3) represent the relational/time-series database entities migrated during Phase 0 database setup:
    1. Project Vision & Locked Configuration Enforcement (`1–2`)
    2. Non-Promissory Financial Risk Disclosures & Brand Identity (`3–4`)
    3. UI/UX Design System & 3 Theme Concepts (`A`, `B`, `C`) (`5–6`)
    4. Website 18-Module Sitemap & Responsive Layout Shells (`7–8`)
    5. Frontend Architecture (Next.js/React, TypeScript, Tailwind CSS, Lightweight Charts) (`9–10`)
    6. Backend Service Architecture (Python FastAPI, Pydantic v2, SQLAlchemy 2.0, Alembic, Redis, Celery, WebSockets) (`11–12`)
    7. Database Architecture: 3 TimescaleDB Hypertables + 28 Regular PostgreSQL Tables = **31 Total Tables** (`13–14`)
    8. Authentication Pipeline (Argon2id, Session Management, Email Verification, Password Reset, TOTP MFA) (`15–17`)
    9. 5-Tier Role-Based Access Control (`FOUNDER`, `ADMIN`, `PRIVATE_TESTER`, `FREE_USER`, `PREMIUM_USER`) (`18–19`)
    10. Founder Control Panel & Admin Operational Console (`20–21`)
    11. 9-Timeframe Market Data Ingestion (`1M`–`1MO`) for `XAUUSD` & `BTCUSD` with DST Session Clocks & Calendar-Aware Monthly Gap Detection (`22–24`)
    12. Standardized Data Integrity Badges (`DATA UNAVAILABLE`, `NOT CONNECTED`, `MARKET_CLOSED`, `STALE`) (`25`)
    13. 24-Control Security Matrix, Rate Limiting, & Immutable Audit Logging (`26–28`)
    14. Docker Multi-Container Orchestration, CI/CD Pipeline, Structured Telemetry, & Encrypted Backup/DR Runbooks (`29–32`)
- **Explicit Phase 0 Constraint:** Phase 0 **must not** implement trading intelligence, 12-brain calculations, SMC detectors, or signal generation.
- **Acceptance Criteria:** All 31 database tables migrate cleanly with TimescaleDB hypertable composite PKs; RBAC prevents Admin from overriding Founder locks; market data service validates or reports `NOT CONNECTED`/`DATA UNAVAILABLE`/`MARKET_CLOSED` for all 9 timeframes on `XAUUSD` and `BTCUSD`; 100% of Phase 0 unit and security tests pass.

---

### PHASE 1 — QUANTUM 12-BRAIN INTELLIGENCE CORE
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Implement the 12 independent analytical brains across `XAUUSD` and `BTCUSD` for all 9 timeframes (`1M`–`1MO`).
- **Non-Circular Dependency Contract Between Phase 1 and Phase 2 (`ISMCStateProvider` / `SMCAnalysisSnapshot`):**
  - **Dependency Analysis:**
    - **4 Self-Contained Price/Indicator Brains (`Brains 1, 9, 10, 11`)** compute directly from confirmed `market_candles` OHLCV series + session clock metadata without requiring Phase 2 SMC objects (`Brain 1: Trend`, `Brain 9: Momentum`, `Brain 10: Volume & Displacement`, `Brain 11: Volatility & Session`).
    - **7 Structure/Liquidity/POI Brains (`Brains 3, 4, 5, 6, 7, 8, 12`)** evaluate institutional SMC primitives (`BOS`/`CHoCH`/`MSS`, `BSL`/`SSL`/`EQH`/`EQL` 7-state liquidity pools, Sweeps, 6-state `OB`/`BB`/`MB`, `FVG`/`IFVG`, and Dealing Range Premium/Discount).
    - **1 Multi-Timeframe Brain (`Brain 2`)** aggregates confirmed HTF trend, structure, liquidity, and POI states from Phase 3 MTF snapshots.
  - **How Circular Dependency Is Eliminated:**
    1. **Typed Interface Contract (`SMCAnalysisSnapshot` Pydantic Schema):** Phase 1 defines an immutable, strictly typed `SMCAnalysisSnapshot` data contract (containing confirmed `external_structure`, `internal_structure`, `dealing_range`, `liquidity_pools` in their 7 lifecycle states, `order_blocks` in their 6 lifecycle states, and `fvg_zones`).
    2. **Stage 1A (Phase 1 Core):** Implement the `BrainEvaluationResult` orchestrator, the `SMCAnalysisSnapshot` interface contract, the 4 self-contained brains (`Brains 1, 9, 10, 11`), and the decision/voting rule evaluators for `Brains 2–8, 12` tested against deterministic `SMCAnalysisSnapshot` fixtures.
    3. **Stage 2 (Phase 2 SMC Engine):** Implement the live 26-concept stateful `smc_service` detector that populates `SMCAnalysisSnapshot` and persists `smc_analyses` on every confirmed candle close.
    4. **Runtime Per-Candle Execution Order (Strictly Topological, Zero Cycles):** On every confirmed candle close $t$, the runtime pipeline always executes in strict topological order:
       $$\text{Step 1: Ingest Confirmed Candle } t \longrightarrow \text{Step 2: Run Phase 2 SMC Detector (`smc_service`)} \longrightarrow \text{Step 3: Run Phase 3 MTF Cutoff Sync (`mtf_service`)} \longrightarrow \text{Step 4: Run All 12 Brains (`brains_service`)}$$
- **Scope & Deliverables:**
  - Implement Brains 1 through 12 as isolated, stateless/deterministic Python modules adhering to the unified `BrainEvaluationResult` Pydantic contract:
    1. `BRAIN_01_TREND` (Trend Intelligence — with 200–249 warm-up & `1MO` macro profile)
    2. `BRAIN_02_MTF` (Multi-Timeframe Intelligence — `NEUTRAL` in Mode A; 2-HTF / 1-HTF `1W` / 0-HTF `1MO` in Mode B)
    3. `BRAIN_03_STRUCTURE` (Market Structure)
    4. `BRAIN_04_LIQUIDITY_MAP` (Liquidity Mapping — reads 7-state liquidity lifecycle)
    5. `BRAIN_05_LIQUIDITY_SWEEP` (Liquidity Sweep — reads `RAIDED_UNDER_EVALUATION` & `SWEPT_RECLAIMED` states)
    6. `BRAIN_06_REVERSAL_TRAP` (Reversal and Trap Detection)
    7. `BRAIN_07_ORDER_BLOCK` (Order Block Analysis — reads 6-state OB/BB/MB lifecycle)
    8. `BRAIN_08_FVG` (Fair Value Gap)
    9. `BRAIN_09_MOMENTUM` (Momentum Intelligence)
    10. `BRAIN_10_VOLUME_DISPLACEMENT` (Volume and Displacement — with missing-volume abstention & price-only cap)
    11. `BRAIN_11_VOLATILITY_SESSION` (Volatility and Session — contiguous `[0, 100]` percentile partition & IANA DST clocks)
    12. `BRAIN_12_PRECISION_ENTRY` (Precision Entry)
  - Separate voting (`BUY`, `SELL`, `NEUTRAL`, `ABSTAIN_DATA_UNAVAILABLE`) from confidence (`0.00–100.00`).
  - Persist evaluations in `brain_analyses` and `brain_votes` tables.
- **Acceptance Criteria:** Deterministic unit tests pass for every brain across all 9 timeframes and both markets; missing data reliably triggers `ABSTAIN_DATA_UNAVAILABLE` with zero fake votes; zero duplicate indicator counting across brains.

---

### PHASE 2 — INSTITUTIONAL AND SMC INTELLIGENCE
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Implement the 26 institutional Smart Money Concepts (`BOS`, `CHoCH`, `MSS`, Internal/External Structure, Swing Highs/Lows, `BSL`, `SSL`, `EQH`/`EQL`, Sweeps, Stop-Hunt Proxies, Liquidity Pools, `OB`, `BB`, `MB`, `FVG`, `IFVG`, Displacement, Imbalances, Premium/Discount, Equilibrium, Dealing Range, Inducement, Supply/Demand, Session Liquidity, `PDH`/`PDL`, `PWH`/`PWL`).
- **Scope & Deliverables:**
  - Build the stateful/event-driven SMC lifecycle engine implementing the **7-State Liquidity Pool Lifecycle** (Section 11.2 Brain 4/5) and **6-State Order Block Lifecycle** (Section 11.2 Brain 7) across all 9 timeframes.
  - Populate the `SMCAnalysisSnapshot` contract consumed by Brains 3–8, 12, persist snapshots in `smc_analyses`, and expose REST/WebSocket telemetry to UI chart overlays.
- **Acceptance Criteria:** Every one of the 26 SMC features passes confirmation, invalidation, non-repainting pivot delay (`r` right-bars confirmed), and timeframe-isolation unit tests.

---

### PHASE 3 — MULTI-TIMEFRAME INTELLIGENCE
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Build the 9-timeframe synchronization and alignment engine supporting both Mode A (Independent Timeframe Signals) and Mode B (MTF Confirmed Signals).
- **Scope & Deliverables:**
  - Implement the non-duplicating Execution-to-HTF/LTF mapping matrix for `1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W` (`HTF 1 = 1MO`, `HTF 2 = NULL`), and `1MO` (`HTF 1 = NULL`, `HTF 2 = NULL`).
  - Implement the 6-dimensional alignment evaluator (Trend, Structure, Liquidity, SMC, Momentum, Volatility) and conflict detector.
  - Enforce the strict `htf_close_timestamp <= exec_close_timestamp` non-repainting cutoff rule.
- **Acceptance Criteria:** Zero lookahead bias verified via bar-by-bar sequential replay tests; conflicting HTF conditions reliably trigger `has_conflict = TRUE` in Mode B.

---

### PHASE 4 — MASTER DECISION ENGINE
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Combine Phases 1, 2, and 3 (plus hooks for Phase 5 & 6 gates) into the `STRICT` Equal-Voting Master Decision Engine outputting `BUY`, `SELL`, or `WAIT`.
- **Scope & Deliverables:**
  - Implement the 6-Gate evaluation pipeline, minimum voting threshold verification (Mode A 11-voter pool vs. Mode B 12-voter pool), mandatory core brain confirmation, conflict detection, duplicate signal suppression, and lifecycle invalidation tracking.
  - Populate all 18 mandatory signal attributes (including `quality_grade`) in `signals` and `signal_history`.
- **Acceptance Criteria:** Every evaluation cycle produces a complete 18-field signal record with an explicit human-readable explanation for every `BUY`, `SELL`, and `WAIT` decision; signals from one timeframe never leak into another timeframe.

---

### PHASE 5 — EXECUTION AND RISK MANAGEMENT
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Calculate structural Entry Zones (Sniper & Fast Scalper), Stop Loss (including the 3-priority Fast Scalper SL hierarchy), `TP1`/`TP2`/`TP3`, Partial Profit, Break-Even, Trailing Stop, Position Sizing, and enforce portfolio risk circuit breakers.
- **Scope & Deliverables:**
  - Implement `trade_plans` and `risk_records` calculators with separate configurations per market (`XAUUSD` vs. `BTCUSD`), timeframe (`1M`–`1MO`), and strategy.
  - Enforce Daily Loss Limit, Max Drawdown halt, Consecutive Loss protection, Max Open Positions, Correlated Risk limit, Spread/Slippage protection, and Emergency Stop kill switch.
- **Acceptance Criteria:** Any setup violating minimum `R:R`, spread ceiling, or daily/max drawdown limits is vetoed into `WAIT`; position size math matches verified contract specifications to 6 decimal places.

---

### PHASE 6 — NEWS INTELLIGENCE AND MARKET PROTECTION
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Integrate macroeconomic and market-specific news intelligence (`CPI`, `NFP`, `FOMC`, `PCE`, `GDP`, Unemployment, Gold macro drivers, Bitcoin regulatory/ETF/exchange/funding drivers) and enforce automated market protection circuit breakers.
- **Scope & Deliverables:**
  - Build economic calendar ingestion & countdown service (`news_events` table), source reliability scoring, actual-vs-forecast delta tracking, and **fail-closed `NEWS_DATA_UNAVAILABLE` handling** (Section 16.3).
  - Implement automated protection freezes for High-Impact News windows, Abnormal Volatility shocks, Spread spikes, Low Liquidity rollover windows, **Market-Calendar-Aware Stale Data Detection** (`MARKET_CLOSED` vs. `STALE`, Section 17.2), and Feed Failures with hysteresis recovery validation.
- **Acceptance Criteria:** Simulated Tier-1 news windows, news feed disconnections, stale candle feeds, and spread spikes immediately force the Master Decision Engine into `WAIT` and recover only after recovery validation rules pass.

---

### PHASE 7 — WEBSITE AND TRADINGVIEW INTEGRATION
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Deliver the complete 18-module web application interface, TradingView Pine Script v6 indicator/strategy script, authenticated webhook pipeline, and modular future broker adapter interfaces.
- **Scope & Deliverables:**
  - Implement all 18 website dashboards using the Founder-approved UI theme (Concept A, B, or C).
  - Develop the non-repainting **Pine Script v6** script supporting `XAUUSD` and `BTCUSD` across all 9 timeframes with explicit `"1"` $\leftrightarrow$ `"1M"` and `"1M"` $\leftrightarrow$ `"1MO"` mapping, `[1]` closed-bar `request.security()` tuple retrieval, on-chart SMC drawings, `BUY`/`SELL`/`WAIT` labels, Entry/SL/TP1/TP2/TP3 lines, heads-up dashboard table, and 18-field JSON webhook alerts.
  - Connect and verify 6-layer authenticated webhook ingestion (`POST /api/v1/webhooks/tradingview`).
- **Acceptance Criteria:** Full functional parity between backend rules and Pine Script v6 (within documented TradingView platform constraints); every UI interactive control works across desktop and mobile viewports with zero mock data fabrication.

---

### PHASE 8 — BACKTESTING, TESTING AND OPTIMIZATION
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Validate the complete QUANTUM intelligence system across historical and forward market data on `XAUUSD` and `BTCUSD` across all nine timeframes (`1M`–`1MO`).
- **Scope & Deliverables:**
  - Run comprehensive historical backtests, market regime tests (Bull, Bear, Sideways, High-Volatility Shock), session tests (Asian, London, NY), In-Sample, Out-of-Sample, Walk-Forward, and Parameter Sensitivity tests.
  - Incorporate realistic spread and slippage simulation models.
  - Execute automated Lookahead-Bias tests, Repainting tests, and Signal Consistency tests (comparing backend vs. Pine Script v6 outputs).
  - Compute and store all 9 mandatory performance metrics (`Win Rate`, `Profit Factor`, `Expectancy`, `Average R`, `Maximum Drawdown`, `Recovery Factor`, `Average Trade Duration`, `TP/SL Hit Rate`, `Consecutive Losses`) reported strictly separately per market, timeframe, and strategy mode.
- **Acceptance Criteria:** Zero lookahead bias or repainting detected; full empirical backtest ledger generated from real historical data without any invented performance numbers.

---

### PHASE 9 — PRIVATE LAUNCH AND PUBLIC RELEASE
- **Status:** `PLANNED` (`NOT IMPLEMENTED`)
- **Purpose:** Execute controlled Private Beta validation with Founder and invitation-based testers, complete security/recovery audits, and prepare the platform for optional Founder-approved Public Release.
- **Scope & Deliverables:**
  - **Stage 9A (Private Beta):** Founder access, invitation-based Private Tester onboarding, in-app feedback & bug reporting loop, real-time paper-trading forward validation.
  - **Stage 9B (Production Hardening & Legal/Compliance):** Penetration & security review, production deployment verification, monitoring alerts, encrypted backup & disaster recovery drill, Privacy Policy, Terms of Service, and explicit Financial Risk Disclosure.
  - **Stage 9C (Public Release Gate):** Complete Public Release Checklist. Public registration remains locked until explicit Founder sign-off.
- **Acceptance Criteria:** All Private Beta exit gates, backup restoration drills, legal disclosures, and security audits pass; explicit Founder `APPROVED` record logged before enabling public access.

---

## 28. Phase Dependencies & Non-Circular Execution Graph

### 28.1 Development Build Sequence vs. Runtime Per-Candle Execution Sequence

```text
================================================================================
A. DEVELOPMENT PHASE BUILD ORDER (FOUNDER-GATED STEP-BY-STEP SEQUENCE)
================================================================================
[PHASE 0: Foundation, 31-Table DB Migration, RBAC, 9-TF Ingestion, UI Shell]
       │
       ▼
[PHASE 1 (Stage 1A): BrainEvaluationResult Contract + SMCAnalysisSnapshot Schema
  + Self-Contained Brains (1, 9, 10, 11) + Fixture-Tested Rule Engines (3..8, 12)]
       │
       ▼
[PHASE 2: Live 26-Concept SMC Stateful Engine (7-State Liquidity & 6-State OB)
  Populating SMCAnalysisSnapshot + Full Live Wiring of Brains 3, 4, 5, 6, 7, 8, 12]
       │
       ▼
[PHASE 3: 9-Timeframe MTF Synchronization Engine + Brain 2 (Mode A & Mode B)]
       │
       ├──────────────────────────┬──────────────────────────┐
       ▼                          ▼                          ▼
[PHASE 5: Execution &      [PHASE 6: News Intel &     [PHASE 4: STRICT Master
 Risk Management Engine]    Market Protection Guards]  Decision Engine (Gates 1..6)]
       │                          │                          │
       └──────────────────────────┼──────────────────────────┘
                                  ▼
         [PHASE 7: 18-Module Website UI & TradingView Pine Script v6]
                                  │
                                  ▼
         [PHASE 8: Backtesting, Walk-Forward, Repainting & Bias Verification]
                                  │
                                  ▼
         [PHASE 9: Private Beta Launch ──► (Founder Gate) ──► Public Release]

================================================================================
B. RUNTIME PER-CANDLE TOPOLOGICAL EXECUTION PIPELINE (ZERO CIRCULARITY)
================================================================================
Confirmed Candle Close (Symbol, Timeframe, t_close)
  ──► 1. Ingestion & Calendar/Session Gap Validator (Section 25.2)
  ──► 2. Phase 6 Market Protection & Fail-Closed News Check (Sections 16 & 17)
  ──► 3. Phase 2 SMC Stateful Detector -> emits SMCAnalysisSnapshot(t_close)
  ──► 4. Phase 3 MTF Cutoff Sync (t_HTF_close <= t_close) -> emits MTFAnalysisSnapshot(t_close)
  ──► 5. Phase 1 Twelve Brains Evaluator (Brains 1..12 run in parallel over Snapshots)
  ──► 6. Phase 4 Master Decision Engine (Gates 1..5 Tally & Conflict Check)
  ──► 7. Phase 5 Execution & Risk Planner (Gate 6 Entry/SL/TP1-3 & Drawdown Check)
  ──► 8. Persist 18-Field SignalRecord + Broadcast via WebSocket / Outbound Webhook
```

---

## 29. Testing Architecture

Every major feature and phase must pass a 5-layer automated verification suite before being presented to the Founder for review:

| Test Layer | Scope & Tooling | Mandatory Verification Targets |
| :--- | :--- | :--- |
| **1. Unit Tests** | `pytest` (Python Backend) & `vitest` (TypeScript Frontend) | Individual testing of all 12 brains, all 26 SMC detectors (including 7-state liquidity and 6-state OB transitions), position sizing formulas, Fast Scalper 3-priority SL math, and `1M` vs. `1MO` / Pine `"1"` vs. `"1M"` mapping validators using deterministic OHLCV fixtures. |
| **2. Non-Repainting & Lookahead-Bias Tests** | Custom Quantitative Replay Harness | Feeds historical candles sequentially one bar at a time ($t_1, t_2, \dots, t_N$) and asserts that the decision, brain votes, and HTF state emitted at bar $t_k$ are 100% identical to those produced when running over the full array $[t_1 \dots t_N]$. Any discrepancy fails the build immediately. |
| **3. Integration & Database Tests** | `pytest-asyncio` + Testcontainers (PostgreSQL/TimescaleDB & Redis) | Verifies TimescaleDB hypertable composite primary keys (`market_candles`, `system_logs`, `api_logs`), relational foreign keys (`signals -> brain_analyses`), append-only `audit_logs` triggers, calendar-aware `1MO` leap-year gap detection, and Gate 1–6 decision persistence. |
| **4. End-to-End (E2E) & UI State Tests** | Playwright | Tests RBAC route protection (verifying Admin cannot access Founder controls), timeframe switching across all 9 timeframes (`1M`–`1MO`), Mode A vs. Mode B toggling, and proper rendering of `DATA UNAVAILABLE`, `NOT CONNECTED`, `MARKET_CLOSED`, and `STALE` states. |
| **5. Security & Static Analysis** | `ruff`, `mypy`, `bandit`, `pip-audit`, `gitleaks`, `tsc --noEmit` | Zero type errors, zero hardcoded secrets, SQL injection prevention, and TradingView webhook 6-layer secret/nonce/timestamp rejection tests. |

---

## 30. Backtesting, Walk-Forward, and Optimization Framework

Phase 8 enforces institutional quantitative validation standards to prevent curve-fitting and survivorship/lookahead bias:

1. **Isolated 9-Timeframe & Dual-Market Execution:**
   - Every backtest runs and reports results independently for a specific `(symbol, execution_timeframe, signal_mode, strategy_version)` tuple.
   - `XAUUSD 5M Mode B` metrics are never averaged together with `BTCUSD 4H Mode A` metrics.
2. **Market Regime & Session Segmentation:**
   - Segments historical performance across:
     - **Market Regimes:** Trending Bullish, Trending Bearish, Sideways Range, High-Volatility Expansion, Low-Volatility Compression.
     - **Trading Sessions:** Asian Session, London Session, London/NY Overlap, New York Afternoon, and Weekend (for `BTCUSD`).
3. **In-Sample, Out-of-Sample, and Walk-Forward Protocol:**
   - **In-Sample (`IS`, e.g., 60% window):** Used for initial parameter calibration.
   - **Out-of-Sample (`OOS`, e.g., 20% untouched holdout window):** Evaluates generalization on unseen data.
   - **Rolling Walk-Forward Analysis (`WFA`):** Sliding rolling windows (`e.g., 6-month IS calibration -> 2-month OOS forward test`) to measure parameter stability over changing macro cycles.
   - **Parameter Sensitivity Testing:** Perturbs key thresholds ($\pm 10\%, \pm 20\%$) across a neighborhood grid; rejects fragile "cliff-edge" parameter peaks that collapse under minor variation.
4. **Realistic Microstructure Friction Simulation:**
   - Models dynamic session-adjusted bid-ask spreads (including wider spreads during rollover/volatility) and execution slippage on stop/market triggers.
5. **Nine Mandatory Performance Metrics (Computed Strictly from Actual Runs — Never Fabricated):**
   - **Win Rate (%):** $\frac{\text{Winning Trades}}{\text{Total Closed Trades}} \times 100$
   - **Profit Factor:** $\frac{\sum \text{Gross Winning P\&L}}{\left|\sum \text{Gross Losing P\&L}\right|}$
   - **Expectancy (in R and Currency):** $(P_{\text{win}} \times \text{Avg Win R}) - (P_{\text{loss}} \times \text{Avg Loss R})$
   - **Average R Multiple:** Mean realized $R$ across all closed trades
   - **Maximum Drawdown (% and R):** Peak-to-trough equity decline
   - **Recovery Factor:** $\frac{\text{Net Profit}}{\text{Maximum Drawdown}}$
   - **Average Trade Duration:** Mean holding time from entry trigger to final exit
   - **TP / SL Hit Rate Breakdown:** Percentage of trades hitting `TP1`, `TP2`, `TP3`, `Break-Even`, `SL`, or `Invalidated/Expired`
   - **Maximum Consecutive Losses:** Longest streak of consecutive losing trades

---

## 31. Deployment, Hosting, and Infrastructure

### 31.1 Three-Tier Environment Architecture
1. **Development (`dev`):** Local containerized environment (`docker-compose.dev.yml`) with hot-reloading, isolated test database, and historical test fixtures (explicitly badged `DEMO / HISTORICAL FIXTURE DATA`).
2. **Staging / Pre-Production (`staging`):** Production-mirror environment running live market data feeds, paper-trading forward validation, and webhook ingestion tests prior to Founder phase sign-off.
3. **Production (`prod`):** Hardened, private-by-default cloud deployment with automated backups, strict firewall/WAF rules, TLS 1.3 termination, and Founder-gated release controls.

### 31.2 Docker Container Architecture
The full system is orchestrated via multi-stage, non-root Docker containers:
- `quantum-reverse-proxy`: Nginx / Traefik handling TLS 1.3, rate limiting, security headers, and WebSocket upgrade routing.
- `quantum-web`: Next.js / React frontend container.
- `quantum-api`: FastAPI async REST & WebSocket server container.
- `quantum-worker-realtime`: High-priority Celery worker dedicated to 9-timeframe candle ingestion and live 12-brain/decision evaluation.
- `quantum-worker-backtest`: Resource-capped Celery worker dedicated to Phase 8 historical backtests.
- `quantum-scheduler`: Celery Beat scheduler triggering timeframe boundary checks and economic calendar syncs.
- `quantum-db`: PostgreSQL 16 + TimescaleDB container with persistent encrypted volume mounts.
- `quantum-redis`: Redis 7 container with AOF persistence for state caching and task queues.

### 31.3 CI/CD Pipeline
- Automated pipeline executing on every commit/PR:
  `Secret Scan (gitleaks)` $\rightarrow$ `Lint & Typecheck (ruff, mypy, eslint, tsc)` $\rightarrow$ `Dependency CVE Audit` $\rightarrow$ `Unit & Non-Repainting Replay Tests` $\rightarrow$ `Database Migration Test` $\rightarrow$ `Docker Image Build`.
- **Production Deployment Gate:** Continuous Deployment to `prod` is never automatic; it requires a manual workflow approval gate triggered only after the Founder writes `APPROVED`.

---

## 32. Logging, Monitoring, and Observability

- **Structured JSON Logging:** Every log entry emitted by Frontend, API, Workers, and Database jobs is formatted as structured JSON containing `timestamp_utc`, `service`, `environment`, `trace_id`, `symbol`, `timeframe`, `event_code`, and `severity` (redacting all passwords, tokens, and PII).
- **System Health & Data Telemetry Monitors:**
  - **Candle Ingestion Lag Monitor:** Alerts if any of the 9 timeframes on `XAUUSD` or `BTCUSD` misses a scheduled confirmed candle close beyond the grace threshold (while suppressing false alerts during `MARKET_CLOSED` windows).
  - **Brain Evaluation Latency Monitor:** Tracks execution duration of the 12-brain + SMC + MTF pipeline (target `< 250ms` per confirmed candle close).
  - **Provider Quota & Error Monitor:** Tracks 429 rate-limit responses and WebSocket reconnections per market data provider.
  - **Resource & Queue Depth Monitor:** Tracks CPU, memory, TimescaleDB disk usage, and Celery realtime vs. backtest queue backlog.

---

## 33. Backup, Disaster Recovery, and Business Continuity

| Recovery Metric / Procedure | Target Specification |
| :--- | :--- |
| **Recovery Point Objective (`RPO`)** | `< 15 minutes` via continuous PostgreSQL Write-Ahead Log (`WAL`) archiving + daily full `pg_dump` / TimescaleDB snapshots. |
| **Recovery Time Objective (`RTO`)** | `< 30 minutes` full infrastructure provisioning and automated database restoration from encrypted off-site object storage. |
| **Backup Encryption & Retention** | All snapshots encrypted via `AES-256-GCM`; daily backups retained 30 days, weekly backups retained 6 months, monthly backups retained 2 years. |
| **Automated Backup Validation & Recovery Drills** | Scheduled monthly verification job that restores the latest encrypted backup into an isolated ephemeral container, runs row-count and checksum integrity queries against `users`, `strategy_versions`, `signals`, and `audit_logs`, and logs verification proof. |
| **Market Data Gap Self-Healing** | Upon system restart after any downtime window, the `ingestion_service` queries the last confirmed timestamp per `(symbol, timeframe)` across all 9 timeframes, backfills all missed candles from the REST provider before unlocking live signal evaluation, and logs `RECOVERY_VALIDATION_PASSED`. |

---

## 34. Founder Approval System & Governance

### 34.1 Mandatory Step-by-Step Phase Execution Protocol
Every future interaction in this project is governed by the following 10-step protocol:
1. **Founder Prompt:** The Founder provides a specific Phase or sub-phase instruction.
2. **Strict Scope Adherence:** Engineering work executes **only** on the explicitly approved scope of that prompt.
3. **Implementation:** Complete the requested tasks cleanly without altering locked configurations.
4. **Testing:** Run all relevant automated tests (unit, integration, non-repainting, lint/compile).
5. **Evidence Reporting:** Provide verifiable test outputs and execution evidence.
6. **Issue Disclosure:** Explicitly list any known errors, edge cases, or technical limitations.
7. **Incomplete Work Disclosure:** Explicitly report any unfinished items within the scope.
8. **Hard Stop:** Stop all tool execution and wait for Founder review.
9. **Founder Verdict:** Founder reviews the deliverable and either approves or rejects it.
10. **Gate Unlock:** Advancement to the next step occurs **only** when the Founder explicitly writes **`APPROVED`** and provides or authorizes the next instruction.

### 34.2 Official Project Status Vocabulary
All deliverables, modules, and phase checklists must use these ten standardized status labels accurately:
- `PLANNED`: Documented in roadmap, awaiting design/prompt.
- `DESIGNED`: Architectural and technical specification completed.
- `APPROVED`: Explicitly approved by the Founder.
- `IMPLEMENTED`: Source code / configuration written.
- `TESTED`: Automated tests executed with recorded output.
- `VERIFIED`: Implementation + tests confirmed passing against all acceptance criteria.
- `NOT IMPLEMENTED`: Not yet built in code.
- `NOT VERIFIED`: Built or drafted, but not yet verified by executed tests.
- `BLOCKED`: Halted by an external dependency, missing credential, or conflicting requirement.
- `PENDING FOUNDER DECISION`: Requires an explicit choice or parameter authorization from the Founder.

---

## 35. Known Limitations & Technical Risks

| # | Limitation / Technical Risk | Root Cause & System Impact | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **1** | **TradingView Pine Script v6 Sandbox & Webhook Constraints** | Pine Script v6 cannot make arbitrary outbound HTTP requests to fetch live macroeconomic news calendars (`CPI`, `NFP`, `FOMC`), enforces hard limits on drawing objects (`500` boxes/lines) and `request.security()` calls (`40`), and TradingView's webhook dispatcher cannot compute dynamic HTTP header HMAC signatures over request bodies. | Pine Script bundles HTF series into 2 non-repainting `[1]` closed-bar `request.security()` tuple calls and embeds a 256-bit `webhook_secret` + `event_nonce` in the JSON payload. The Python backend enforces 6-layer webhook verification, applies Phase 6 live fail-closed News Protection, and cross-verifies against backend candle state. |
| **2** | **No Proprietary Interbank Level-3 Order-Flow Data** | True institutional central-bank/prime-broker order books are non-public. | QUANTUM models institutional footprints algorithmically via OHLCV displacement, liquidity sweep kinematics, tick/exchange volume (`RVOL`), and SMC structural shifts without making false claims of proprietary bank order-book access. |
| **3** | **Decentralized `XAUUSD` Pricing, DST Shifts & Tick Volume Variance** | Spot Gold (`XAUUSD`) trades OTC across multiple liquidity providers; high/low wicks and tick volume vary slightly across feeds, and NY `17:00` close shifts between `21:00 UTC` (EDT) and `22:00 UTC` (EST). | Parameterize symbol tolerances in `ATR` multiples, enforce IANA `America/New_York` DST-aware timezone conversion across all services, store `provider_id` and `volume_type` on every candle, and apply Brain 10's missing-volume abstention/cap rules. |
| **4** | **Licensing & Redistribution Costs of Commercial Market Data** | Most low-latency market data providers permit private/internal use on low-cost tiers but require paid commercial redistribution agreements before displaying live charts to public paying users. | Maintain `Initial Access: Private` through Phases 0–8; verify commercial data redistribution licensing as a mandatory gate item in the Phase 9 Public Release Checklist. |
| **5** | **`1MO` (Monthly) Timeframe MTF Hierarchy Ceiling & `BTCUSD` Historical Depth (`< 200` Monthly Bars in Bitcoin's History)** | `1MO` is the highest of the 9 timeframes (`HTF 1 = NULL, HTF 2 = NULL`), and Bitcoin has only traded since 2009–2011 (`~183–195` total monthly bars in existence, fewer than `200` bars for a standard 200-month EMA). | On `1MO`, Brain 2 uses the `TOP_OF_HIERARCHY_NO_HTF` (`NEUTRAL`) rule; `BTCUSD` stitches early 2011 Bitstamp/index history with live USD feeds; and Brain 1 activates the explicit `1MO_MACRO_PROFILE` (`EMA 12/24/60`, requiring `>= 60` monthly bars) when `60 <= N < 200` on `1MO`, while keeping the strict `>= 200` bar floor on `1M`–`1W`. |
| **6** | **Current Workspace Template vs. Target Multi-Service Stack** | The current repository contains a lightweight Vite + React 19 + TypeScript + Tailwind CSS v4 + Express (`tsx`) scaffold (Section 38.2), whereas the target blueprint architecture specifies a multi-container Python FastAPI + PostgreSQL 16/TimescaleDB + Redis + Celery + React/Next.js topology. | Explicitly documented in Section 38.2 and tracked under `PFD-08` so the Founder controls the exact Phase 0 runtime topology before any code is written. |

---

## 36. Pending Founder Decisions

In strict compliance with Section 4 and Section 12 of the Master Instruction, no assumptions have been silently hardcoded for the items below. Each item has a complete, production-ready baseline engineered in this blueprint while remaining explicitly marked **`PENDING FOUNDER DECISION`** for final Founder confirmation:

| Decision ID | Decision Topic | Engineered Baseline in Blueprint & Options for Founder Confirmation | Status |
| :--- | :--- | :--- | :--- |
| **PFD-01** | **Default Execution Timeframe on Dashboard Load** | All 9 timeframes (`1M`, `5M`, `15M`, `30M`, `1H`, `4H`, `1D`, `1W`, `1MO`) are fully supported. Confirm default initial timeframe selected on UI startup (`15M` proposed baseline, or `5M` / `1H`). | `PENDING FOUNDER DECISION` |
| **PFD-02** | **UI Design Theme Selection** | Select one of the three documented themes (Section 18.1):<br>• **Concept A:** Black + Gold — Premium Institutional<br>• **Concept B:** Black + Electric Blue — Futuristic AI<br>• **Concept C:** Black + Neon Green — Trading Terminal | `PENDING FOUNDER DECISION` |
| **PFD-03** | **Minimum Brain Voting Threshold (`STRICT` Mode)** | Engineered baseline in Section 14.2: Minimum `8` directional votes (`8/11` active voters in Mode A; `8/12` in Mode B) with at most `1` opposing vote, minimum `72.00%` aggregate confidence, and minimum `9` non-abstaining brains. Confirm baseline or custom threshold. | `PENDING FOUNDER DECISION` |
| **PFD-04** | **Primary & Fallback Market Data Providers** | Select primary and fallback data providers for `XAUUSD` and `BTCUSD` from Section 25.3 (e.g., OANDA v20 / Twelve Data / Polygon.io for `XAUUSD`; Coinbase/Kraken/Bitstamp/Polygon true `BTC-USD` + Binance secondary telemetry for `BTCUSD`). | `PENDING FOUNDER DECISION` |
| **PFD-05** | **Economic Calendar & News Data Provider Selection** | Select primary structured economic calendar feed for Phase 6 (`CPI`, `NFP`, `FOMC`, `PCE`, `GDP`) and crypto news/funding endpoints (system enforces fail-closed `NEWS_DATA_UNAVAILABLE` if unconfigured in live mode). | `PENDING FOUNDER DECISION` |
| **PFD-06** | **`XAUUSD` Daily (`1D`) & `4H` Candle Alignment Mode** | Engineered baseline in Sections 5.2 & 6.4: `XAUUSD` `1D` closes at `17:00 America/New_York` (`21:00 UTC` EDT / `22:00 UTC` EST) while `4H` uses `UTC_MODULO_4H` (`00:00, 04:00, 08:00, 12:00, 16:00, 20:00 UTC`). Confirm baseline or select `NY_SESSION_4H` / `00:00 UTC` daily close. | `PENDING FOUNDER DECISION` |
| **PFD-07** | **Baseline Risk & Circuit-Breaker Thresholds** | Engineered baseline in Section 15: Risk Per Trade (`0.50%` Fast Scalper / `1.00%` Sniper), Daily Loss Limit (`2.00%`), Max Drawdown (`6.00%`), Consecutive Losses (`3` reduces risk 50%, `4` halts 24h), and minimum `R:R` floors (`1.5R` Scalper, `2.0R` Sniper). Confirm or adjust. | `PENDING FOUNDER DECISION` |
| **PFD-08** | **Phase 0 Frontend/Backend Runtime Topology** | Confirm whether Phase 0 should scaffold the multi-container Python FastAPI + PostgreSQL/TimescaleDB + Redis + React/Next.js stack or adapt within the AI Studio container runtime (`Vite + React 19 + Node/Python bridge`). | `PENDING FOUNDER DECISION` |

---

## 37. Future Expansion & Modular Broker Adapters

While **Initial Auto Trading is Disabled** by locked configuration, QUANTUM is architected so future execution and expansion modules can plug into the Phase 4/5 outputs without modifying the core intelligence brains:

1. **Abstract Execution Adapter Interface (`IBrokerExecutionAdapter`):**
   - Defines standard methods: `get_account_summary()`, `get_symbol_specification()`, `get_live_spread()`, `validate_order_margin()`, `place_bracket_order(trade_plan)`, `modify_stop_loss()`, `close_partial_position()`, and `emergency_flatten_all()`.
   - Future adapter implementations (disabled behind `feature_flags` until approved by Founder):
     - MetaTrader 5 (`MT5`) / cTrader Bridge Adapter (for `XAUUSD` & CFD brokers).
     - REST/FIX Crypto Exchange Adapter (e.g., Binance, Bybit, Coinbase Advanced, Kraken for `BTCUSD`).
     - Paper-Trading Internal Simulation Adapter (active in Phases 5–9 for zero-risk forward validation).
2. **Additional Markets & Asset Classes:**
   - Because market microstructure, session hours, tick values, and news drivers are data-driven via `market_symbols` and `strategy_versions`, future markets (e.g., `EURUSD`, `NAS100`, `ETHUSD`, `XAGUSD`) can be onboarded by adding symbol profiles without rewriting the 12-brain engine.

---

## 38. Current Project Status, Actual Repository Structure & Target Blueprint Structure

### 38.1 Current Project Status Summary

| Project Component | Official Status Label | Notes |
| :--- | :--- | :--- |
| **Master Project Blueprint (`README.md`)** | `DESIGNED` (`Version 1.1`) | Complete post-audit specification documented in root `README.md`; awaiting Founder review. |
| **Phase 0 — Foundation & Architecture** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 1 — 12-Brain Intelligence Core** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 2 — Institutional & SMC Intelligence** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 3 — Multi-Timeframe Intelligence** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 4 — Master Decision Engine** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 5 — Execution & Risk Management** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 6 — News Intelligence & Market Protection** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 7 — Website & TradingView Integration** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 8 — Backtesting, Testing & Optimization** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |
| **Phase 9 — Private Launch & Public Release** | `NOT IMPLEMENTED` | Documented; awaiting Founder prompt & approval. |

### 38.2 Actual Current Repository File Tree & Installed Packages (As of Blueprint Version 1.1)
In accordance with the strict documentation-only rules of this blueprint phase, **zero application code, database migrations, or backend folders have been created yet**. The physical repository currently contains only the initial AI Studio workspace template plus this root `README.md`:

```text
/                                             # Actual Current Repository Root
├── .env.example                              # Template env vars (GEMINI_API_KEY, APP_URL)
├── .gitignore                                # Git ignore rules
├── README.md                                 # QUANTUM Master Project Blueprint (Version 1.1 — ONLY modified file)
├── index.html                                # Initial Vite HTML entry point (unmodified placeholder)
├── metadata.json                             # AI Studio applet metadata (unmodified placeholder)
├── package.json                              # Initial Node.js package manifest (React 19, Vite 8, Tailwind 4, Express 4)
├── tsconfig.json                             # TypeScript compiler config
├── vite.config.ts                            # Vite bundler configuration
└── src/
    ├── App.tsx                               # Empty React placeholder component (returns <div></div>)
    ├── index.css                             # Tailwind CSS v4 import (@import "tailwindcss";)
    └── main.tsx                              # React DOM root mount
```

- **Currently Installed Workspace Packages (`package.json`):**
  - `dependencies`: `react` (`^19.0.1`), `react-dom` (`^19.0.1`), `vite` (`^8.3.0`), `@vitejs/plugin-react` (`^6.1.1`), `@tailwindcss/vite` (`^4.3.3`), `lucide-react` (`^0.546.0`), `motion` (`^12.23.24`), `express` (`^4.21.2`), `dotenv` (`^17.2.3`), `@google/genai` (`^2.4.0`).
  - `devDependencies`: `typescript` (`^7.0.2`), `tsx` (`^4.21.0`), `tailwindcss` (`^4.3.3`), `autoprefixer` (`^10.4.21`), `esbuild` (`^0.25.0`), `@types/react`, `@types/react-dom`, `@types/express`, `@types/node`.
- **Current Implementation State:** `0%` of QUANTUM trading logic, database tables, backend services, or UI dashboards are implemented in the files above.

### 38.3 Intended Target Blueprint Repository & Folder Structure (Phases 0–9)
*(None of the target directories below exist yet; they will be created strictly phase-by-phase upon Founder `APPROVED` prompts starting in Phase 0.)*

```text
/
├── README.md                                 # Master Project Blueprint (Current File)
├── docker-compose.yml                        # Future multi-service container orchestration
├── .env.example                              # Environment variable template (no secrets)
├── docs/                                     # Future detailed phase & architecture records
│   ├── adr/                                  # Architecture Decision Records
│   ├── phases/                               # Phase 0–9 test evidence & Founder approval logs
│   ├── api/                                  # OpenAPI & WebSocket contract documentation
│   └── runbooks/                             # Backup, recovery, and incident runbooks
├── backend/                                  # Future Python FastAPI Intelligence Backend
│   ├── app/
│   │   ├── main.py                           # FastAPI application entrypoint
│   │   ├── core/                             # Config, security, Argon2id, JWT/session, RBAC, logging
│   │   ├── db/                               # SQLAlchemy 2.0 models (31 tables: 3 hypertables + 28 relational) & Alembic
│   │   ├── ingestion/                        # XAUUSD & BTCUSD 9-TF adapters, DST clocks & calendar-aware gap detector
│   │   ├── brains/                           # Phase 1: 12 independent analytical brain modules (01..12)
│   │   ├── smc/                              # Phase 2: 26 institutional & SMC detectors (7-state liquidity, 6-state OB)
│   │   ├── mtf/                              # Phase 3: 9-timeframe alignment & non-repainting cutoff sync
│   │   ├── decision_engine/                  # Phase 4: STRICT Equal-Voting Master Decision Engine (18-field SignalRecord)
│   │   ├── risk/                             # Phase 5: Entry/SL/TP1-3 (incl. 3-priority Fast Scalper SL), sizing, circuit breakers
│   │   ├── news_protection/                  # Phase 6: Fail-closed economic calendar, Gold/BTC catalysts, market guards
│   │   ├── backtesting/                      # Phase 8: Bar-by-bar replay, WFA, lookahead/repaint tests
│   │   ├── adapters/                         # Modular future broker execution adapters
│   │   ├── api/v1/                           # REST routes, 6-layer TradingView webhook handler, WebSocket hub
│   │   └── workers/                          # Celery realtime & backtest worker tasks
│   └── tests/                                # Unit, SMC, MTF lookahead, security, and integration tests
├── frontend/                                 # Future Web Application (18 Sitemap Modules)
│   ├── src/
│   │   ├── components/                       # Design system UI tokens, charts, 12-brain cards, tables
│   │   ├── features/                         # 18 dashboard feature modules (XAUUSD, BTCUSD, Founder, etc.)
│   │   ├── hooks/                            # WebSocket stream hooks & 9-timeframe state selectors
│   │   ├── services/                         # Strictly typed API client
│   │   └── types/                            # Shared TypeScript interfaces (18-field SignalRecord & '1M'..'1MO' enums)
│   └── tests/                                # Vitest unit tests & Playwright E2E tests
└── tradingview/                              # Future Phase 7 Pine Script v6 Integration
    ├── quantum_intelligence_v6.pine          # Non-repainting Pine Script v6 indicator/alert script
    └── webhook_payload_schema.json           # 18-field JSON schema for TradingView -> Backend webhook validation
```

---

## 39. Development Workflow & Change Control

### 39.1 Strict Step-by-Step Workflow
1. **Read & Verify Blueprint:** Every development session begins by reading this Master `README.md`.
2. **Wait for Phase Prompt:** The Founder provides a specific Phase or sub-phase prompt.
3. **Scope Isolation:** Work strictly on the approved scope of that prompt—never jump ahead to subsequent phases or unrequested files.
4. **Execute & Test:** Complete the work, run the verification test suite, and capture empirical test evidence.
5. **Comprehensive Status Report:** Report completed work, incomplete work, errors, technical limitations, and test results using the official status labels (`IMPLEMENTED`, `TESTED`, `VERIFIED`, `NOT IMPLEMENTED`, `PENDING FOUNDER DECISION`, etc.).
6. **Stop and Wait:** Halt completely and wait for Founder review.
7. **Explicit Founder Approval Required:** Proceed to the next step **only** when the Founder explicitly writes **`APPROVED`** and authorizes the next instruction.

### 39.2 Conflict Resolution & Change Control Protocol
Approved requirements in this blueprint must never be silently overwritten. If any future prompt or technical discovery conflicts with an approved requirement in this Master Blueprint:
1. **Explain the Conflict:** Clearly identify which locked requirement or blueprint section is affected.
2. **Explain the Impact:** Detail the technical, analytical, risk, or security consequences across `XAUUSD`, `BTCUSD`, the 9 timeframes, or the 12 brains.
3. **Present Alternatives:** Provide structured options with trade-offs.
4. **Wait for Founder Decision:** Stop and wait for the Founder's explicit ruling before modifying the blueprint or code.

### 39.3 Blueprint Version History

| Blueprint Version | Date (UTC) | Author / Authority | Summary of Changes | Approval Status |
| :--- | :--- | :--- | :--- | :--- |
| **`1.0`** | `2026-11-19` | Engineering System (Under Founder Authority) | Initial creation of complete QUANTUM Trading Intelligence Master Project Blueprint (`README.md` only). Documented Phases 0–9, 9 timeframes (`1M`–`1MO`), 12 brains, 26 SMC concepts, MTF architecture, Master Decision Engine, Risk & News Protection, 31 database entities, 24 security controls, 3 UI concepts, and Founder governance rules. | Superseded by `1.1` |
| **`1.1`** | `2026-11-19` | Engineering System (Post-Audit Technical Revision) | Completed comprehensive 26-point technical audit and cross-section synchronization:<br>1. **TimescaleDB Hypertables (Section 22):** Classified 3 hypertables (`market_candles`, `system_logs`, `api_logs`) with composite PKs containing their partitioning timestamp column (`(symbol_id, timeframe, timestamp)` and `(created_at, id)`), and 28 regular relational tables (`brain_analyses`, `signals`, etc.) so foreign keys and unique constraints migrate cleanly.<br>2. **Non-Duplicating 9-Timeframe MTF Matrix & Brain 2 Rules (Sections 8, 9, 11, 13, 14):** Corrected `1W` (`HTF 1 = 1MO`, `HTF 2 = NULL`) and `1MO` (`HTF 1 = NULL`, `HTF 2 = NULL`, `TOP_OF_HIERARCHY_NO_HTF`); defined Brain 2 as `NEUTRAL` in Mode A (11 active directional voters) and mandatory in Mode B (12 voters for `1M`–`1W`; `1MO` top-of-hierarchy exception).<br>3. **Unified 7-State Liquidity Lifecycle & 6-State OB Lifecycle (Sections 11.2, 12):** Resolved Brain 4 vs. Brain 5 sweep/reclaim contradiction via 7 deterministic states (`CREATED`, `ACTIVE_UNMITIGATED`, `RAIDED_UNDER_EVALUATION`, `SWEPT_RECLAIMED`, `INVALIDATED_BROKEN_BOS`, `CONSUMED_ARCHIVED`, `EXPIRED`) and resolved Brain 7 50% MT vs. Distal Edge rules via 6 OB states (`UNMITIGATED_FRESH`, `MITIGATED_SHALLOW_ACTIVE`, `MITIGATED_DEEP_ACTIVE` [-30pt penalty], `MITIGATED_CONSUMED`, `INVALIDATED`, `CONVERTED_TO_BREAKER_BLOCK` / `MITIGATION_BLOCK`).<br>4. **Pine Script v6 Non-Repainting MTF & Timeframe Mapping (Sections 6, 19):** Added canonical multi-provider interval mapping (`1M` $\leftrightarrow$ Pine `"1"`, `1MO` $\leftrightarrow$ Pine `"1M"`) and non-repainting `[1]` closed-bar tuple `request.security()` retrieval.<br>5. **IANA DST Session Clocks, 4H Alignment & Calendar-Aware Monthly Gaps (Sections 5, 6, 11, 17, 25):** Replaced static `21:00 UTC` assumption with `America/New_York` (`21:00 UTC` EDT / `22:00 UTC` EST) and `Europe/London` IANA clocks, defined `UTC_MODULO_4H` vs. `NY_SESSION_4H`, and implemented calendar-aware `relativedelta(months=+1)` leap-year gap detection.<br>6. **Brain 1, 10, 11, Fast Scalper SL, 18-Field Signal Schema, Fail-Closed News, Stale Data, Webhook Security, `1MO` History & Phase 1/2 Order (Sections 7, 11, 14–17, 22–25, 27–28, 38):** Reconciled 200 vs. 250 bar warm-up tiers and `1MO` macro profile; Brain 10 missing-volume abstention & 70% price-only cap; Brain 11 contiguous `[0, 100]` percentile partition; 3-priority Fast Scalper SL; 18th signal field `quality_grade` across all schemas; fail-closed `NEWS_DATA_UNAVAILABLE`; market-calendar-aware `MARKET_CLOSED` vs. `STALE` detection; 6-layer realistic TradingView webhook security; `BTCUSD` vs. `BTCUSDT` basis normalization; non-circular Phase 1/2 `SMCAnalysisSnapshot` contract; and actual vs. target repository tree. | `PENDING FOUNDER DECISION` (Awaiting Founder Review) |

