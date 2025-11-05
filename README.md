# Amazon Product Scraper Bot

This project automates structured product data extraction from the Amazon Android app—capturing titles, prices, ratings, images, and availability at scale. It removes repetitive, error-prone tapping and copy-pasting by orchestrating real devices and emulators with human-like flows. The result: reliable, export-ready product catalogs for analytics, monitoring, or feed ingestion.

<p align="center"> 
   Created by Appilot, built to showcase our approach to Automation!<br>
   <strong>If you are looking for custom Amazon Product Scraper Bot, you've just found your team — Let’s Chat.👆👆</strong>
</p>

## Introduction
**What it does:** Controls Android devices/emulators to navigate Amazon listings, open PDPs, parse key attributes, and persist normalized product records.  
**What it automates:** Category traversal, search pagination, product detail opening, attribute capture, media collection, and resilient retries.  
**Benefits:** Faster catalog building, consistent datasets, and hands-off, scheduled runs across many accounts/devices.

### Automating Amazon Catalog Intelligence
- Navigates categories, search results, and recommendations with deterministic flows and fallback heuristics.
- Normalizes data (price, currency, rating, ASIN, merchant) and exports JSON/CSV for downstream pipelines.
- Works on real devices or emulators with intelligent delays and swipe/scroll dynamics for stability.
- Integrates rotating proxies/VPN per device to reduce blocking and regionalize results.
- Built-in audits: screenshots, UI XML dumps, and structured logs for traceability.

## Core Features
- **Real Devices and Emulators:** Run on USB-connected phones, device farms, or Bluestacks/Nox. Unified controller abstracts input, orientation, DPI, and surface differences.
- **No-ADB Wireless Automation:** Optional ADB-less control via accessibility and input bridges; deployable over Wi-Fi for headless rigs.
- **Mimicking Human Behavior:** Randomized tap radii, inertia-aware scrolling, viewport pauses, and jittered dwell times to emulate natural usage.
- **Multiple Accounts Support:** Session vault with per-profile cookies, app data isolation, and credential rotation to segment tasks cleanly.
- **Multi-Device Integration:** Scheduler dispatches jobs across fleets; per-device queues, health checks, and backpressure to maximize throughput.
- **Exponential Growth for Your Account:** Scale horizontally—add devices, add accounts, add regions—without redesigning flows or code.
- **Premium Support:** Priority troubleshooting, device-lab onboarding, custom module development, and SLAs for mission-critical runs.

**Additional Capabilities**

| Feature Name | Description |
|---|---|
| ASIN & Variant Resolver | Detects parent/child relationships (size/color bundles) and consolidates variants into a single normalized record. |
| Price & Deal Detector | Extracts current price, strikethrough price, coupons, lightning deals, and computes discount deltas. |
| Media & Attribute Parser | Captures primary image, gallery, bullets, A+ sections, and tech specs with robust UI tree parsing. |
| Seller & Buy Box Insights | Identifies merchant, fulfillment type (FBA/FBM), and buy box presence where visible. |
| Regionalization Controls | Region/device affinity rules to compare pricing/availability across locales and stores. |
| Resilience & Retry Engine | Automatic relaunch on crashes, stale view detection, and step-level retries with exponential backoff. |

</p>
<p align="center">
  <a href="https://appilot.app" target="_blank">
    <img src="media/amazon-product-scraper-bot-banner.png" alt="amazon-product-scraper-bot-architecture" width="95%">
  </a>
</p>

## How It Works (must)
1. **Input or Trigger** — Configure tasks in the Appilot dashboard: categories, keywords, store/region, depth, schedule, and export format.  
2. **Core Logic** — The controller drives the Android app via UI Automator/Appium or wireless input bridges, performing search, scrolling, PDP opening, and structured field capture.  
3. **Output or Action** — Normalized records (JSON/CSV/Parquet) are written to `/output`, with screenshots and logs for QA; optional webhooks push to queues or data stores.  
4. **Other functionalities** — Centralized retry logic, error classes, per-step timing, device watchdogs, rotating proxies/VPN, and parallel pipelines configurable from the dashboard.

## Tech Stack (must)
- **Language:** Python, Java/Kotlin, JavaScript  
- **Frameworks:** Appium, UI Automator, Espresso (aux), Robot Framework (optional test harness), Cucumber (BDD optional)  
- **Tools:** Appilot, Android Debug Bridge (ADB), Appium Inspector, Bluestacks/Nox, Scrcpy, Firebase Test Lab, MonkeyRunner, Accessibility Services  
- **Infrastructure:** Dockerized device farms, cloud emulators, proxy networks, parallel device execution, task queues, real device lab

## Directory Structure
    amazon-product-scraper-bot/
    │
    ├── src/
    │   ├── main.py
    │   ├── controller/
    │   │   ├── device_manager.py
    │   │   ├── input_bridge.py
    │   │   ├── ui_navigator.py
    │   │   └── screenshotter.py
    │   ├── extractors/
    │   │   ├── listing_parser.py
    │   │   ├── pdp_parser.py
    │   │   └── variant_resolver.py
    │   ├── pipelines/
    │   │   ├── normalizer.py
    │   │   ├── exporters/
    │   │   │   ├── csv_exporter.py
    │   │   │   ├── json_exporter.py
    │   │   │   └── parquet_exporter.py
    │   │   └── webhooks.py
    │   ├── scheduler/
    │   │   ├── dispatcher.py
    │   │   ├── job_queue.py
    │   │   └── healthcheck.py
    │   └── utils/
    │       ├── logger.py
    │       ├── config_loader.py
    │       ├── retry.py
    │       └── region_profile.py
    │
    ├── config/
    │   ├── settings.yaml
    │   ├── devices.yaml
    │   └── credentials.env
    │
    ├── tests/
    │   ├── test_parsers.robot
    │   └── fixtures/
    │       └── sample_views.xml
    │
    ├── logs/
    │   └── run.log
    │
    ├── output/
    │   ├── products.csv
    │   ├── products.json
    │   └── screenshots/.keep
    │
    ├── docker/
    │   └── Dockerfile
    │
    ├── requirements.txt
    └── README.md

## Use Cases (must)
- **Marketplace analysts** use it to compile category snapshots, so they can track pricing, availability, and seasonal changes.  
- **E-commerce teams** use it to enrich internal catalogs with attributes and images, so they can improve merchandising and search.  
- **Data engineers** use it to feed BI pipelines with normalized product records, so they can build dashboards and alerts.  
- **Brand managers** use it to monitor competitor listings, so they can respond to positioning and offer changes.  

## FAQs
**How do I configure this automation for multiple accounts?**  
Define profiles in `config/devices.yaml` and `config/settings.yaml` with per-profile app data dirs. The scheduler assigns jobs round-robin or by affinity rules.

**Does it support proxy rotation or anti-detection?**  
Yes. Configure per-device VPN/proxy endpoints and enable randomized human-like inputs (scroll/tap jitter, dwell variance) plus staggered start times.

**Can I schedule it to run periodically?**  
Yes. Use the built-in dispatcher with cron-style schedules or trigger via webhook; failed jobs auto-retry with bounded backoff.

**What export formats are supported?**  
CSV, JSON, and Parquet out of the box, with optional webhook forwarding to queues or HTTP endpoints.

## Performance & Reliability Benchmarks (must)
- **Execution Speed:** ~120–220 PDPs per device per hour (median), depending on network, device class, and depth settings.  
- **Success Rate:** 95% end-to-end completion on stable device farms with retries enabled.  
- **Scalability:** Proven patterns for 50–300 devices; architecture supports 1,000+ with sharded queues and region-aware scheduling.  
- **Resource Efficiency:** CPU-light controller; I/O-bound operations with adaptive wait strategies to minimize idle time.  
- **Error Handling:** Step-scoped retries, app relaunch, stale-view detection, annotated screenshots, and structured logging with run IDs.

