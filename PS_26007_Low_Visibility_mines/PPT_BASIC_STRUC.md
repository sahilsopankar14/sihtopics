# SLIDE 1 — TITLE PAGE

## SMART INDIA HACKATHON 2026

- **Problem Statement ID:** SIH26007
- **Problem Statement Title:** Safe and Efficient Operation of Mine Vehicles in Fog and Low-Visibility Conditions in Open Cast Iron Ore Mines
- **Ministry:** Ministry of Steel
- **Organisation:** NMDC
- **Theme / PS Category:** Hardware / Smart Automation
- **Team ID:** [Insert]
- **Team Name:** [Insert]

---

# SLIDE 2 — INNOVATION AND UNIQUENESS + PROPOSED SOLUTION / APPROACH

## DRISHTI
*Restoring Situational Awareness When Visibility Fails*

## Innovation and Uniqueness

- **Purpose-Driven Sensor Fusion:** Each sensor is assigned one specific job instead of stacking technologies — radar for ranging, camera for classification, GPS/map for road context.

- **Fog-Resilient Detection:** Combines radar's fog-penetration strength with camera-based classification to overcome the individual blind spots of each sensor.

- **AI Applied Only Where Justified:** AI is used solely for tasks a fixed threshold cannot reliably perform — object classification, tracking, and confidence scoring.

- **Predictive Road-Context Alerts:** Digital map + GPS warn of curves and hazard zones before they are visually visible, ahead of camera detection range.

- **Graceful Degradation Design:** Local safety functions continue operating during network loss; events are cached and synced once connectivity returns.

- **Fleet-Wide Situational Awareness:** Extends beyond single-vehicle safety into a control-room view of all equipped vehicles simultaneously.

## Proposed Solution / Approach

- **Multi-Sensor Perception Layer:** Radar, camera, GPS and IMU continuously capture vehicle surroundings and motion state.

- **Sensor Fusion Engine:** Combines imperfect individual sensor outputs into a single reliable object identity and confidence estimate.

- **Collision Risk Engine:** Calculates distance, relative speed and time-to-collision to classify risk as Low / Medium / High.

- **Driver Alert System:** Delivers a simple 3-tier signal — Green (Safe), Yellow (Caution + distance), Red (Danger + object + brake prompt).

- **Control-Room Dashboard:** Provides a live fleet map, active alerts and real-time visibility/weather status.

- **Fail-Safe Operation:** Ensures the safety function continues even if communication or a single sensor is temporarily lost.

**Diagram:** Sense → Fuse → Detect → Track → Predict Risk → Alert → Monitor

---

# SLIDE 3 — TECHNICAL APPROACH

## Components / Technology Stack to be Used

- **Radar:** Object ranging and relative-speed detection; robust performance in fog and low visibility.

- **Camera:** Visual classification of detected objects (person / vehicle / obstacle).

- **GPS + IMU:** Vehicle location, heading, speed and digital road-map context.

- **Edge Computing Unit:** On-vehicle processing for sensor fusion, detection and risk calculation with minimal latency.

- **AI Perception Module:** Object classification, multi-frame tracking and confidence scoring.

- **Communication Link (V2I):** Transmits alerts and vehicle status to the control-room dashboard.

- **Control-Room Software:** Fleet map, live alerts, visibility monitoring and event logging.

## Implementation Process

- **Sensing:** Radar, camera, GPS and IMU capture raw environmental and vehicle data in real time.

- **Sensor Fusion:** Combines multi-sensor inputs to resolve individual sensor blind spots and reduce false detections.

- **AI Perception:** Classifies detected objects and tracks their motion across frames.

- **Risk Calculation:** Computes distance, relative speed and time-to-collision to assign a risk level.

- **Driver Alert:** Issues a simple colour-coded, audio-visual warning suited for in-cab operation.

- **Fleet Monitoring:** Logs events and updates the control-room dashboard for fleet-wide awareness.

**Diagram:** Input → Sensor Fusion → AI Perception → Risk Engine → Alert → Control Room

---

# SLIDE 4 — FEASIBILITY AND VIABILITY

| Feasibility | Viability | Practical Implementation |
|---|---|---|
| Built on established sensor categories already used in vehicle ADAS systems | Fail-safe design keeps core safety function active during network loss | Deployment path: prototype → single vehicle → pilot mine → fleet scale-up |
| Sensor fusion directly compensates for each sensor's individual fog/rain weakness | Minimal driver interface requires no training beyond colour-alert recognition | System designed to complement, not replace, existing DGMS-recognised safety controls |
| AI applied only to tasks that genuinely require it, reducing system complexity | Graceful degradation ensures safety continuity during connectivity gaps | Scales from single-vehicle pilot to full fleet deployment |

## Potential Challenges and Risks

- **01 — Sensor degradation:** Individual sensors (LiDAR, camera) lose reliability in dense fog, rain or dust.
- **02 — Connectivity gaps:** Mine environments may lack consistent network coverage for real-time sync.
- **03 — False negatives:** A missed detection is far more dangerous than a false alarm.
- **04 — Alert fatigue:** Excessive warnings can reduce driver responsiveness over time.
- **05 — Training data scarcity:** Real Indian mine fog datasets for AI training may be limited.

## Strategies for Overcoming Challenges

- **01:** Multi-sensor fusion ensures no single point of sensing failure.
- **02:** Local processing continues operating offline; data syncs once reconnected.
- **03:** System design prioritises minimising missed detections over reducing false alerts.
- **04:** Minimal 3-tier colour-coded interface limits cognitive load on the driver.
- **05:** Controlled fog-chamber testing with measured visibility levels supplements limited real-world data.

---

# SLIDE 5 — IMPACT AND BENEFITS

## Target Audience

- **Driver / Operator:** Receives earlier, simpler hazard information without needing to read a complex display.

- **Control Room / Mine Operator:** Gains a single fleet-wide view of vehicle positions, alerts and visibility conditions.

- **NMDC / Mining Company:** Potential reduction in fog-related unnecessary slowdowns and improved fleet coordination.

- **Haul-Road Workers:** Earlier detection in person-crossing scenarios improves on-ground worker safety.

## Benefits of the Solution

- **Safety:** Improves situational awareness and provides earlier, more reliable hazard warnings under low-visibility conditions.

- **Operational:** Reduces uncertainty-driven vehicle slowdowns and supports more consistent haul-road movement during fog.

- **Economic:** Supports better fleet utilisation by reducing avoidable stoppages during adverse weather.

- **Social:** Strengthens protection for on-ground workers operating alongside heavy mine vehicles.

> *"The system is designed to improve situational awareness and reduce collision risk — not to claim elimination of accidents."*

---

# SLIDE 6 — RESEARCH AND REFERENCES

## Field & Applied Research

Compilation of documented mine-vehicle and low-visibility incident records to identify recurring accident patterns.

## Academic & Government Sources

- **DGMS Annual Report (2024):** States that dumpers, tippers, trucks and similar vehicles were involved in 36% of fatal accidents analysed in 2023 in opencast coal mines, with run-over, being-hit, head-on collision and toppling identified as recurring categories.

- **DGMS — Transportation Safety Provisions:** Documented safety interventions on wheeled trackless transportation machinery, covering collision, reversing and rear-vision safety measures.

- **NMDC Annual Reports:** Primary organisational source for mine operations and safety context.

- **Problem Statement Reference:** Bailadila mines reporting visibility as low as 3–5 metres during severe monsoon conditions.