# SIH26007 — Pre-Commitment Research Report
## Safe and Efficient Operation of Mine Vehicles in Fog and Low-Visibility Conditions in Open Cast Iron Ore Mines
**Problem Statement:** SIH26007
**Ministry:** Ministry of Steel
**Organization:** NMDC
**Category:** Hardware / Smart Automation
**Core domain:** Mining safety + intelligent transportation + sensor fusion + AI/ML + IoT + driver assistance

## 1. Problem Definition
Before considering LiDAR, radar, AI, cameras, dashboards, or related technologies, the problem can be stated as follows:

A huge mining vehicle has to travel on a mine haul road, but during severe fog its driver cannot see far enough ahead to safely operate the vehicle at normal/efficient speeds.
The problem is therefore not simply “fog.”
The underlying operational problem is:
Low visibility → reduced situational awareness → increased uncertainty → driver slows/stops or may fail to detect hazards → collision/accident risk increases → haulage efficiency decreases → production is affected.
The official problem statement says Bailadila can experience visibility as low as 3–5 metres during severe monsoon conditions. (SIH Fit)
The operating scenario is represented below:

             DUMPER
        ┌──────────────┐
        │    DRIVER    │
        └──────┬───────┘
               │
               │  ONLY 3–5 m VISIBILITY
               ↓
        ????? ????? ????
        ????? ????? ????
               ↓
        Another dumper
        Worker/person
        Road curve
        Obstacle
        Road edge
The driver may not have sufficient information to make a safe decision.

## 2. Failure Scenarios
The accident mechanism must be understood by the complete project team.
The statement:

“Fog causes accidents.”
does not by itself describe how the accident occurs. The accident mechanism is as follows.

### Scenario A — Vehicle ahead
The dumper under consideration
     ↓
   🚛  ───────────────→

              🚛
        Vehicle ahead
The vehicle is travelling at, for example, 20–25 km/h.
Because of fog:

driver cannot see far ahead
another dumper is moving/stopped
driver notices it too late
braking distance is not enough
collision occurs
The system should therefore answer:
“Is there an object/vehicle ahead, how far away is it, how fast is it moving, and is the current situation dangerous?”

## 3. Scenario B — Human/person ahead
The scenario consists of a worker crossing the haul road.

                 👷
                 ↑
                 │
        🚛 ──────┼────────→
             YOUR DUMPER
The camera may see something.
Radar may detect something.
But the important question becomes:

What is that thing?
It could be:

person
vehicle
rock
tree
barrier
equipment
dust/fog artifact
This is where AI can become useful.

## 4. Rationale for AI
The requirement for AI should be established independently of the inclusion of AI/ML in the SIH problem statement.
A simple radar provides the following example.
Radar says:

Object detected at 30 m.
That's already useful.
The following rule could be written:

IF object_distance < 20m
    THEN WARNING
No AI required.
However, consider the following combined observations:

Radar:
Object at 32 m

Camera:
Something appears in front

Thermal:
Heat signature detected

GPS:
Vehicle travelling at 23 km/h

Vehicle telemetry:
Current heading = 15°
Now the system has multiple pieces of information.
AI/ML can help answer questions such as:

“What is the object?”
“Is it probably a human?”
“Is it probably another vehicle?”
“Is the object actually moving?”
“Is this a false detection?”
“What is the system's confidence level?”
“What is the likelihood of collision?”
That is where AI becomes meaningful.

## 5. Functional Distinction
The system has three distinct functions. These functions should not be conflated.

### Job 1 — SENSING
Hardware asks:

“What is physically around me?”
Examples:

radar
LiDAR
camera
thermal camera
GPS
IMU

### Job 2 — PERCEPTION / INTERPRETATION
Software/AI asks:

“What is being observed?”
Examples:

Object detected
       ↓
Is it a vehicle?
       ↓
Is it a human?
       ↓
Is it a rock?
       ↓
Is it moving?
       ↓
Where is it?

### Job 3 — DECISION
Software asks:

“What action should be taken?”
Example:

Human detected
       +
Distance = 15 m
       +
Vehicle speed = 25 km/h
       ↓
HIGH COLLISION RISK
       ↓
RED ALERT
       ↓
BUZZER + DISPLAY
       ↓
"STOP / BRAKE"
This constitutes the core system architecture.

## 6. Candidate Solution Architecture
At this stage, the exact hardware should not yet be selected.
A possible architecture is as follows:

              ┌──────────────────────┐
              │      MINE DUMPER     │
              └──────────┬───────────┘
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
     RADAR            CAMERA           GPS/IMU
        │                │                │
        └────────────────┼────────────────┘
                         ↓
                 SENSOR PROCESSING
                         ↓
                  SENSOR FUSION
                         ↓
              OBJECT DETECTION/TRACKING
                         ↓
                RISK CALCULATION
                         ↓
              COLLISION PREDICTION
                         ↓
        ┌────────────────┴──────────────┐
        ↓                               ↓
       DRIVER ALERT                     CONTROL ROOM
        ↓                               ↓
       Display/Buzzer                    Dashboard
       Vibration                         Fleet map
       Voice Alert                       Alerts
This architecture is more specific than the statement:

“The system will use AI + LiDAR + IoT + GPS.”

## 7. Monitoring Requirements
This question should be answered before system construction.
The monitoring system could monitor:

Vehicle-level information
current vehicle location
speed
direction
acceleration
braking
heading
vehicle health/status if available

Environment
visibility
nearby objects
vehicles
workers/persons
road boundaries
obstacles
road curvature
dangerous zones

Risk
distance to object
relative speed
time-to-collision
collision probability
sudden obstacle appearance
unsafe following distance

Fleet
location of all equipped vehicles
vehicle density
vehicles approaching each other
active warnings
repeated dangerous locations

Weather/environment
Potentially:

fog
rainfall
temperature
humidity
visibility

## 8. Driver Information Requirements
The driver should not be required to inspect a complicated dashboard while operating a large dumper.
The driver should receive extremely simple information.
For example:

Green
🟢 SAFE
No immediate hazard

Yellow
🟡 CAUTION

Vehicle detected
Distance: 60 m

Red
🔴 DANGER

PERSON DETECTED
Distance: 18 m

BRAKE

And perhaps:

buzzer
vibration
voice warning
visual warning
The driver should not need to interpret charts.

## 9. Control-Room Dashboard
The control-room dashboard functions as an air-traffic-control view for mine vehicles. Instead of monitoring airplanes, the operator monitors dumpers.
An example is:

             MINE CONTROL ROOM

 ┌─────────────────────────────────────────┐
 │         DIGITAL MINE MAP                │
 │                                         │
 │     🚛 A                                │
 │                🚛 B                     │
 │                                         │
 │                         🚛 C            │
 │                                         │
 └─────────────────────────────────────────┘

 ACTIVE ALERTS
 ─────────────────────────────────────────
 🔴 Dumper B — collision risk
 🟡 Dumper A — low visibility
 🟡 Dumper C — abnormal speed

 WEATHER
 ─────────────────
 Visibility: 8 m
 Fog: HIGH
 Rain: Moderate
The dashboard is useful because the mine operator gets a fleet-wide view rather than only individual drivers.

## 10. AI Model Prediction Tasks
This should be one of the research questions.
Possible AI tasks include:

Object detection
Image
 ↓
AI
 ↓
Person
Vehicle
Rock
Obstacle

Object tracking
Vehicle detected
       ↓
Track it across frames
       ↓
Is it approaching?
Is it moving away?
Is it stationary?

Risk prediction
Potentially:

Distance
+
Relative velocity
+
Vehicle speed
+
Direction
+
Road geometry
        ↓
Risk model
        ↓
LOW / MEDIUM / HIGH

Anomaly detection
The system might learn what normal vehicle behaviour looks like and flag:

abnormal speed
unusual stopping
unexpected movement
unusual route behaviour
However, not every item necessarily belongs in the final prototype.

## 11. LiDAR Definition
LiDAR is defined as follows.
LiDAR = Light Detection and Ranging.
It is a sensor that uses laser/light pulses to measure distances. Conceptually, it is equivalent to distributing thousands of tiny invisible measuring tapes around the vehicle.

                •
           •         •
       •                 •
     •       🚛            •
       •                 •
           •         •
                •
The system measures how long the light takes to return.
It can create a 3D point cloud.
A point cloud is basically:

. . . . . . .
- . . . . . .
.     🚛     .
- . . . . . .
Thousands/millions of points can describe:

road
vehicle
wall
rock
terrain
obstacles
This represents a 3D shape/map.

## 12. LiDAR Limitations
LiDAR uses light.
Fog contains water droplets.
Rain contains water droplets.
Dust contains particles.
Those particles can scatter/reflect the laser.
Therefore:

Heavy fog, rain and dust can degrade LiDAR performance.
Accordingly, the statement:

“LiDAR will be used because it is accurate.”
should be replaced by the research question:

“How does LiDAR behave in Bailadila's actual environmental conditions?”
This is a research question.

## 13. Radar Definition
Radar uses radio waves rather than visible light.
It can be represented as:

RADAR
  ↓
📡 ))))))))))))

              🚛
              ↑
       reflected signal
It can estimate:

distance
relative speed
direction/angle
One major advantage:

Radar generally performs much better than cameras in fog and poor visibility.
That makes radar particularly interesting for this problem.
But radar has limitations too.
It may have difficulty distinguishing exactly what an object is.
For example:

Radar:
"There is something 25 m away."

But what is it?

Person?
Rock?
Vehicle?
Pole?
Another sensor can therefore complement radar.

## 14. Camera
The camera provides the system's visual sensing function.
It can potentially provide rich visual information.
It can identify:

people
vehicles
road signs
road markings
terrain
obstacles
But:

Dense fog severely reduces visual visibility.
So camera alone is not a reliable solution for the exact problem.

## 15. Thermal Camera
Thermal camera detects infrared radiation associated with temperature.
So:

Normal camera:
"What does it look like?"

Thermal:
"What temperature/heat pattern does it emit?"
A human may stand out from the background.
An important limitation is:

Hot machinery and hot rocks can also produce strong thermal signatures.
Therefore:
thermal ≠ automatic human detection.
It needs interpretation and/or sensor fusion.

## 16. GPS
GPS answers:

“What is the vehicle's location?”
It does NOT answer:

“What's 20 metres in front of me?”
Example:

GPS:
Latitude = X
Longitude = Y
Speed = 21 km/h
It can help with:

vehicle tracking
digital maps
route tracking
geofencing
dangerous-zone identification
But GPS alone cannot prevent a collision.

## 17. GPS and Mapping
The combined function becomes more informative when the system knows:

Current location
       ↓
Digital mine map
       ↓
Road ahead curves sharply
       ↓
Curve in 100 metres
       ↓
Driver warning
This can provide predictive warnings.
Instead of waiting for the camera to see the curve, the system already knows:

“There is a sharp bend ahead.”

## 18. V2V Definition
V2V = Vehicle-to-Vehicle communication.
Consider two dumpers:

🚛 A                     🚛 B

     ← wireless communication →
Vehicle A can tell Vehicle B:

My location:
X,Y

Speed:
18 km/h

Direction:
North

Status:
Emergency braking
Vehicle B receives that information.
This is powerful in fog because the vehicles do not have to depend entirely on visual detection.

## 19. V2I Definition
V2I = Vehicle-to-Infrastructure.
Vehicle communicates with infrastructure.
For example:

🚛
 ↓
Wireless
 ↓
📡 Roadside unit
 ↓
🏢 Control room
Infrastructure can provide:

road information
weather information
hazard zones
traffic information
alerts

## 20. Sensor Fusion
Sensor fusion is a central concept for research.
Instead of asking:

“Which single sensor solves fog?”
Ask:

“How can multiple imperfect sensors work together?”
For example:

                 RADAR
                   ↓
             Object = 25m
                   │
                   │
CAMERA ────────────┼──────────── THERMAL
                   │
       Vehicle-looking object
                   │
                   ↓
             SENSOR FUSION
                   ↓
        "Likely vehicle/person"
                   ↓
             RISK ENGINE
                   ↓
              HIGH RISK
                   ↓
              🚨 ALERT
This is potentially the core technical direction of the project.

## 21. Core Engineering Problem
The project should not be defined as:

“An AI system for mines is being developed.”
That's weak.
A stronger definition is:

“A multi-sensor driver-assistance and fleet-awareness system is being developed to maintain situational awareness of mine vehicles when human visibility becomes inadequate.”
This definition assigns a purpose to each system element.

## 22. Research Checklist — Before Commitment
This is the most important section.
Hardware development should not begin until the project team has checked these items.
A. Problem Understanding
- [ ] Can every team member explain the problem in their own words?
- [ ] Can everyone explain why fog is dangerous?
- [ ] Can everyone explain what happens when visibility drops to 3–5 m?
- [ ] Understand what HEMM means.
- [ ] Understand what a haul road is.
- [ ] Understand what a dumper is.
- [ ] Understand the typical mine transportation cycle.
- [ ] Understand loading → transportation → unloading → return.
- [ ] Understand why stopping vehicles affects production.
- [ ] Understand the difference between safety and productivity.
- [ ] Identify exactly what the driver cannot see.
- [ ] Identify exactly what information the driver needs.
- [ ] Identify exactly what decisions the driver has to make.

## 23. Mining Operations Research
- Establish how open-cast iron ore mining works.
- Study Bailadila mines.
- Study Kirandul.
- Study Bacheli.
- Study Donimalai.
- Characterize mine haul roads.
- Characterize mine road geometry.
- Characterize gradients.
- Characterize curves/hairpin bends.
- Identify loading points.
- Identify dumping/unloading points.
- Study mine traffic rules.
- Study HEMM.
- Study dumper sizes.
- Establish typical dumper speeds.
- Establish braking distances.
- Study blind spots.
- Study reversing.
- Study overtaking.
- Study mixed traffic.
- Study interaction between light vehicles and heavy vehicles.
DGMS material is particularly important here because vehicle movement is a recognized safety issue in open-cast mining. DGMS has specifically highlighted wheeled trackless transportation machinery, including dumpers and trucks, and historical guidance has emphasized visibility, haul roads and vehicle safety. (Directorate General of Mines Safety)

## 24. Accident Research
This should be one of the highest-priority research tracks.
The search should not be limited to:

“fog mining accidents.”
Search broadly for:

- Indian open-cast mine accidents
- dumper accidents
- HEMM accidents
- haul-road accidents
- vehicle collision accidents
- run-over accidents
- reversing accidents
- head-on collisions
- vehicle rollover
- blind-spot accidents
- visibility-related accidents
- monsoon mining accidents
- Bailadila accidents
- NMDC safety incidents
- DGMS accident statistics
A particularly useful official source is the DGMS annual report. Its 2024 report states that 36% of fatal accidents analyzed in 2023 in opencast coal mines involved dumpers, tippers, trucks and similar vehicles; among those accidents, it reports run-over, being-hit, head-on collision and toppling categories. (Directorate General of Mines Safety)
Important: This should not be presented as “36% of all Indian mining accidents.” It is specifically the DGMS analysis described in that report. The source context must always be preserved.

## 25. Accident Data Table
Build a research spreadsheet.

| Year | Mine | Vehicle | Accident type | Cause | Visibility/weather | Fatalities | Injuries | Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| YYYY | Mine | Dumper | Collision | Visibility | Fog | XX | XX | DGMS |
| YYYY | Mine | Dumper | Run-over | Human/vehicle | Unknown | XX | XX | DGMS |

The research should compile 20–50 credible incidents.
The resulting data should then be examined for patterns.
The intended evidence-based conclusion is:

“This problem was not invented. Actual incidents were analyzed and recurring failure modes were identified.”

## 26. Existing Safety Systems Research
The research needs to establish:

“What are mines already doing?”
Otherwise, a judge may ask:

“Why is the existing system insufficient?”
Research:

- Rear-view cameras
- Reverse alarms
- Proximity detection
- Collision avoidance systems
- Operator training
- Mine traffic rules
- Speed monitoring
- Fleet management
- GPS tracking
- Radio communication
- Lighting systems
- Fog lights
- Beacon systems
- Radar systems
- Camera systems
- Driver monitoring
- Dispatch systems
DGMS records show that safety provisions already exist around HEMM, rear vision, alarms, haul roads and transportation. Therefore, the solution needs to complement or improve existing controls rather than imply that no existing controls exist. (Directorate General of Mines Safety)

## 27. Competitor / Existing Technology Research
Commercial systems should be identified and researched:

- Mining collision avoidance systems
- Mining proximity detection systems
- Autonomous haul trucks
- Radar-based collision warning
- LiDAR mining systems
- Thermal mining systems
- Mine fleet management
- ADAS for heavy vehicles
- V2V mining systems
- Open-pit mine safety systems
For every system record:

Company
Product
Sensors
Features
Price if available
Deployment environment
Strengths
Weaknesses
What it does not solve
The objective is to identify:

The gap.

## 28. Sensor Research
A separate document should be created.

Camera
Research:

- RGB camera
- low-light camera
- night vision
- camera resolution
- FPS
- field of view
- fog performance
- rain performance
- dust performance

Radar
Research:

- What radar actually measures
- radar frequency bands
- detection range
- angle resolution
- velocity measurement
- fog performance
- rain performance
- dust performance
- false detections
- cost
- availability

LiDAR
Research:

- How LiDAR works
- point cloud
- 2D vs 3D LiDAR
- range
- accuracy
- field of view
- fog limitations
- rain limitations
- dust limitations
- computational requirements
- cost

Thermal
Research:

- Thermal imaging basics
- human detection
- machinery detection
- hot rocks
- temperature differences
- rain/fog effects
- thermal resolution
- cost

GPS/DGPS
Research:

- GPS accuracy
- DGPS accuracy
- RTK GPS
- GPS limitations
- GPS-denied environments
- vehicle tracking
- geofencing
- digital maps

IMU
Learn:

- accelerometer
- gyroscope
- orientation
- vehicle motion
- sensor fusion with GPS

## 29. Sensor Comparison Matrix
The research should eventually produce a matrix such as:

| Requirement | Camera | Radar | LiDAR | Thermal | GPS |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Detect object | Good | Good | Excellent | Good | ❌ |
| Identify person | Excellent | Poor/Moderate | Moderate | Good | ❌ |
| Measure distance | Moderate | Excellent | Excellent | Poor | ❌ |
| Detect speed | Limited | Excellent | Moderate | Poor | Good |
| Fog | Poor | Excellent | Poor/Moderate | Moderate/Good | Excellent |
| Rain | Moderate/Poor | Good | Moderate/Poor | Moderate | Excellent |
| Dust | Poor | Good | Poor | Moderate | Excellent |
| Object classification | Excellent | Limited | Moderate | Good | ❌ |
| Position | ❌ | Relative | Relative | Relative | Excellent |

These ratings should not be copied blindly into the final presentation. They should be validated experimentally and against manufacturer/technical documentation.

## 30. Sensor Fusion Research
This should be a major research topic.
Learn:

- What sensor fusion means
- Early fusion
- Late fusion
- radar + camera fusion
- LiDAR + camera fusion
- GPS + IMU fusion
- Kalman filtering
- object tracking
- multi-object tracking
- confidence scores
- false positives
- false negatives

## 31. AI/ML Research
The research should not be limited to learning “AI.”
It should determine exactly where AI is useful.
Research:

- Object detection
- YOLO
- object classification
- object tracking
- semantic segmentation
- road segmentation
- obstacle detection
- anomaly detection
- collision prediction
- time-to-collision
- sensor fusion ML
- edge AI
- model latency
- model accuracy
- false-positive rate
- false-negative rate

## 32. The Most Important AI Question
Ask:

“What prediction does our AI make that a simple threshold/rule cannot make reliably?”
If this cannot be answered, AI should not be used for that function.
Example:

No AI needed
Radar distance = 10m

IF distance < 15m
→ warning

AI useful
Camera + radar

       ↓

Object detection

       ↓

Person?
Vehicle?
Rock?
Other?

       ↓

Track object

       ↓

Predict movement

       ↓

Collision risk
That distinction will make the project much more technically credible.

## 33. Collision Prediction Research
This is potentially one of the most important areas.
Research:

- stopping distance
- reaction time
- braking distance
- vehicle speed
- relative velocity
- distance
- time-to-collision (TTC)
- trajectory prediction
- road geometry
- vehicle heading
For example:

Vehicle speed = 25 km/h
Distance = 15 m
Object speed = 0
The system needs to determine:

“Is 15 m safe or dangerous?”
Distance alone is not enough.

## 34. Road-Curve Detection
Three approaches should be researched:

Approach 1 — Digital map
GPS location
      ↓
Mine map
      ↓
Curve ahead
      ↓
Warning

Approach 2 — Camera
Camera
 ↓
Road boundaries
 ↓
Curve detection

Approach 3 — LiDAR
LiDAR
 ↓
3D road geometry
 ↓
Road boundary/terrain
The three approaches should then be compared.

## 35. Communication Research
Research:

- Wi-Fi
- LoRa
- private LTE/5G
- RF communication
- V2V
- V2I
- MQTT
- CAN bus
- Ethernet
- edge-to-cloud communication
- offline operation
- communication latency
- packet loss
- communication range

## 36. Hardware Research
The following needs to be determined:

Processing
Possible platforms:

- Raspberry Pi
- NVIDIA Jetson
- ESP32
- Arduino
- STM32
- industrial edge computer

Sensors
- radar
- camera
- GPS
- IMU
- optional LiDAR
- optional thermal

Driver interface
- display
- buzzer
- vibration
- LEDs
- speaker

Communication
- wireless module
- networking
- control-room connection

## 37. Software Research
The software team should investigate:

Edge software
- sensor data acquisition
- preprocessing
- object detection
- object tracking
- sensor fusion
- risk calculation
- alert generation

Backend
- API
- database
- event storage
- vehicle telemetry
- user management

Dashboard
- live map
- vehicle positions
- active alerts
- historical incidents
- vehicle status
- weather/visibility
- analytics

AI
- model training
- dataset
- model deployment
- inference
- edge optimization

## 38. Dataset Research
This could become one of the biggest challenges.
The key question is:

Where will training data be obtained?
Research:

- mining vehicle datasets
- fog datasets
- pedestrian detection datasets
- vehicle detection datasets
- adverse weather datasets
- synthetic fog generation
- custom dataset collection
- simulation
- data augmentation
Actual Indian mine fog datasets may be difficult to obtain.
That itself becomes a major project consideration.

## 39. Prototype Research
Before components are purchased, determine:

What exactly will be demonstrated?
For example:

Miniature mine environment

        🚛
         ↓
   Radar + Camera
         ↓
       Edge PC
         ↓
   Object detection
         ↓
   Collision prediction
         ↓
    🚨 Warning
         ↓
     Dashboard
The prototype should then demonstrate:

Test 1
Vehicle ahead.

Test 2
Person crossing.

Test 3
Obstacle.

Test 4
Fog introduced.

Test 5
Two vehicles approaching.

Test 6
Vehicle suddenly stops.

## 40. Fog Simulation Research
The real environment is difficult to reproduce.
Research:

- fog chamber
- ultrasonic fogger
- water mist
- controlled visibility
- visibility measurement
- camera degradation
- radar performance
- LiDAR performance
The objective is not:

“Smoke has been added.”
The objective is:

“At controlled visibility levels, system behaviour was measured.”
That is much stronger.

## 41. Testing Metrics
Measurable results are required for evaluation.
The following measurement methods should be researched:

Detection
Accuracy
Precision
Recall
F1 score
mAP

System
Detection range
Detection latency
Alert latency
FPS
response time

Safety
Collision warning distance
false alarm rate
missed detection rate
time-to-collision accuracy

Communication
latency
range
packet loss

Hardware
power consumption
operating temperature
battery life

## 42. Cost Research
This is essential because the PS specifically asks for a cost-effective solution.
Create a BOM:

| Component | Quantity | Estimated cost |
| :--- | :--- | :--- |
| Radar | 1 | ₹ |
| Camera | 1 | ₹ |
| GPS | 1 | ₹ |
| IMU | 1 | ₹ |
| Edge computer | 1 | ₹ |
| Display | 1 | ₹ |
| Communication | 1 | ₹ |
| Enclosure | 1 | ₹ |
| Power system | 1 | ₹ |
| Wiring/connectors | — | ₹ |
| **Total** | | **₹** |

The following deployment question should then be evaluated:

Could a mine realistically deploy this on 10, 100 or 500 vehicles?
That is where the project becomes commercially interesting.

## 43. Ruggedization Research
The system is not intended solely for a college laboratory.
It is intended for operation under:

rain
mud
dust
vibration
heat
humidity
mechanical shocks
long operating hours
Research:

- IP ratings
- vibration resistance
- temperature range
- waterproofing
- dust protection
- mounting
- cable protection
- sensor cleaning
- maintenance

## 44. Power Research
Research:

- vehicle power supply
- voltage conversion
- power consumption
- battery backup
- surge protection
- thermal management
- emergency shutdown

## 45. Mine Connectivity Research
The following should not be assumed:

“There will be Wi-Fi everywhere.”
Research actual mine communication conditions.
Ask:

- Is cellular available?
- Is 4G available?
- Is 5G available?
- Is Wi-Fi available?
- Is private network infrastructure available?
- Are there dead zones?
- Can the system work offline?
- What happens if communication fails?
A good system should probably degrade gracefully:

NETWORK AVAILABLE
       ↓
Cloud/control-room sync

NETWORK LOST
       ↓
Local safety system CONTINUES WORKING
       ↓
Data stored locally
       ↓
Sync later
This is an important engineering principle.

## 46. Fail-Safe Research
This is a safety system, so failure matters.
Research:

- What happens if radar fails?
- What happens if camera fails?
- What happens if GPS fails?
- What happens if AI crashes?
- What happens if network fails?
- What happens if sensor gives incorrect data?
- What happens if power drops?
- What happens if system overheats?
The solution should never create a new danger.
For example:

False alert → annoying.
But:

Missed human detection → potentially catastrophic.
Therefore research false negatives carefully.

## 47. Human Factors
The driver is not a robot.
Research:

- Driver workload
- alert fatigue
- too many warnings
- audible warning levels
- visual warning design
- vibration
- voice warnings
- reaction time
- usability
- training requirement
The following question should be answered:

What is the minimum information the driver needs to make the correct decision?

## 48. Regulatory Research
This is another area teams often forget.
Research:

- DGMS regulations
- Coal Mines Regulations where applicable
- metalliferous mine safety requirements
- HEMM safety requirements
- mine traffic rules
- vehicle safety standards
- radio/wireless regulations
- data privacy
- worker monitoring/privacy
- facial recognition implications if it is included
DGMS has specific safety provisions concerning HEMM and wheeled trackless transportation machinery, so regulatory compatibility needs to be part of the research. (Directorate General of Mines Safety)

## 49. Business Model Research
This should be researched, but should not be the center of a technical SIH presentation.
Potential customer:

NMDC / large open-cast mining companies.
Potential model:

Hardware + Software
Hardware installation
        +
Annual software subscription
        +
Maintenance
        +
Analytics
Possible revenue:

hardware sale
installation
software license
annual maintenance
fleet analytics
monitoring platform
sensor replacement
support/training

## 50. Deployment Model
The deployment progression should be defined as follows:

Prototype
   ↓
One vehicle
   ↓
Pilot mine
   ↓
10 vehicles
   ↓
100 vehicles
   ↓
Entire fleet
Research:

- Installation time
- Maintenance
- Calibration
- Training
- Network infrastructure
- Software updates
- Sensor replacement
- Scaling

## 51. Business Case
The business case should not state only:

“It saves lives.”
Also ask:

Does it save money?
Research:

production lost during fog
vehicle downtime
cycle time
fuel consumption
fleet utilization
accident costs
equipment damage
maintenance
operational delays
The business case becomes:

Better visibility
       ↓
Safer operation
       ↓
Less unnecessary slowdown
       ↓
Lower cycle time
       ↓
Higher fleet utilization
       ↓
Higher productivity
Do not invent monetary savings. Calculate them only after obtaining defensible assumptions/data.

## 52. Sustainability
Research:

- fuel savings
- reduced idle time
- efficient haulage
- reduced accident-related waste
- energy consumption of electronics
- maintenance requirements

## 53. Scalability
The following question should be answered:

Can this work only on one demo truck?
If yes, weak.
Better:

1 vehicle
     ↓
10 vehicles
     ↓
100 vehicles
     ↓
500 vehicles
Research how the architecture scales.

## 54. Cybersecurity
Because the system consists of connected vehicles, research:

- encrypted communication
- authentication
- secure device identity
- dashboard authentication
- firmware updates
- network security
- data integrity
- attack prevention
The system must prevent spoofing of the following message:

“Vehicle A is here”
when it is not.

## 55. Questions Judges Will Probably Ask
The project team should prepare answers to these questions.

Problem
Why is this actually a serious problem?
How frequently does it occur?
Who is affected?
How much does it cost?
What happens today?

Existing solutions
What is already being used?
Why is it insufficient?
What is the innovation?

Hardware
Why radar?
Why camera?
Why LiDAR?
Why thermal?
Why not only radar?

AI
Why AI?
What exactly does the model predict?
What dataset was used?
What accuracy was achieved?
What happens if the AI is wrong?

Safety
What happens if the system fails?
What happens if the network fails?
What happens if GPS fails?
What happens if a sensor fails?

Business
Who will buy it?
How much does it cost?
How much does deployment cost?
How does it scale?

Deployment
Can it work in actual mines?
Can it survive dust/rain/vibration?
How will it be installed?
What happens during maintenance?

## 56. Recommended Presentation Structure
A strong structure could be:

Slide 1 — The Problem
“When a 100+ tonne vehicle can see only a few metres ahead, every second becomes a safety decision.”
Then establish the environment.

Slide 2 — Why It Matters
Use credible:

accident statistics
mine production numbers
visibility data
downtime/productivity impact
real incident examples
DGMS is a particularly valuable primary source for safety statistics and regulatory context. Its public dashboard and accident-statistics resources can support this research. (Directorate General of Mines Safety)

Slide 3 — Root Cause
Fog
 ↓
Visibility ↓
 ↓
Situational awareness ↓
 ↓
Late hazard detection
 ↓
Unsafe braking/steering decisions
 ↓
Collision / accident

Slide 4 — Existing Gap
Show:

Current systems
     ↓
GPS
Reverse alarms
Cameras
Rules
Training
     ↓
But...
     ↓
Limited situational awareness
during extreme low visibility
Existing systems should not be described as ineffective unless the research proves it.

## 57. Slide 5 — Proposed Solution
Something like:

Multi-Sensor Intelligent Mine Safety & Mobility System
Radar
Camera
GPS
IMU
Optional thermal/LiDAR
       ↓
Sensor Fusion
       ↓
Object Detection
       ↓
Tracking
       ↓
Collision Risk Engine
       ↓
Driver Alert
       +
Fleet Dashboard

## 58. Slide 6 — Operating Principle
The “automatic door” analogy is useful for explaining this sequence.

1. Sensor detects object
             ↓
2. System estimates distance
             ↓
3. Camera/AI identifies object
             ↓
4. System tracks movement
             ↓
5. GPS/map provides road context
             ↓
6. Risk engine calculates danger
             ↓
7. Driver receives alert
             ↓
8. Control room receives event
             ↓
9. Event is logged

## 59. Slide 7 — AI
The presentation should not state only:

“AI is used.”
Say:

“AI identifies and tracks objects that raw sensors alone cannot reliably classify.”
Then explain:

Raw sensor data
       ↓
AI perception
       ↓
Person / Vehicle / Rock / Obstacle
       ↓
Tracking
       ↓
Risk calculation

## 60. Slide 8 — Hardware
Actual hardware should be shown.

              FRONT
               ↓

          [ CAMERA ]
               |
          [ RADAR ]
               |
        [ GPS + IMU ]
               |
        [ EDGE COMPUTER ]
               |
      ┌────────┴────────┐
      ↓                 ↓
 Driver interface    Communication
                        ↓
                   Control room

## 61. Slide 9 — Software
The following should be shown:

Sensor data
     ↓
Preprocessing
     ↓
AI perception
     ↓
Sensor fusion
     ↓
Object tracking
     ↓
Risk engine
     ↓
Alerts
     ↓
Dashboard

## 62. Slide 10 — Control Room
The demonstration should include:

live vehicle map
vehicle status
alerts
collision risk
visibility
historical events

## 63. Slide 11 — Prototype
The prototype should demonstrate the concept credibly.
The presentation should not claim:

“The system was deployed on a 240-ton dumper.”
Instead, it should state:

“A scaled physical test environment representing the mine scenario was created.”
The demonstration should then include:

Mini haul road
      ↓
Mini dumper
      ↓
Fog
      ↓
Obstacle/person
      ↓
Sensor detection
      ↓
AI classification
      ↓
Collision warning
      ↓
Dashboard

## 64. Slide 12 — Results
This is crucial. Screenshots alone are insufficient.
The presentation should show:

Object detection accuracy: XX%
Detection range: XX m
Alert latency: XX ms
False alarm rate: XX%
Network latency: XX ms
Fog visibility tested: XX m
Actual measured numbers will make the presentation much stronger.

## 65. Slide 13 — Cost
Show:

Prototype cost
Deployment cost
Estimated per-vehicle cost
Maintenance

## 66. Slide 14 — Deployment
Show:

Prototype
 ↓
Pilot vehicle
 ↓
Pilot mine
 ↓
Fleet deployment
 ↓
Multi-mine deployment

## 67. Slide 15 — Business Model
Example:

Hardware
+
Software platform
+
Annual maintenance
+
Analytics
+
Support
Customer:
Mining companies / mine operators
But validate the actual procurement/deployment pathway before presenting this as fact.

## 68. Slide 16 — Impact
Potential metrics:

reduced collision risk
improved driver awareness
reduced unnecessary stoppages
reduced cycle time
improved fleet utilization
improved monitoring
safer monsoon operations
These should be measured or calculated from defensible assumptions. Percentages should not be manufactured.

## 69. The Most Important Research Questions
If the project team has limited time, these questions should be answered first.

Tier 1 — MUST KNOW
- What exactly happens during 3–5 m visibility?
- What are the actual accident mechanisms?
- How many relevant accidents occur?
- What does DGMS say?
- What safety systems already exist?
- What does existing technology fail to solve?
- What information does the driver need?
- Which sensors work in dense fog?
- What can radar actually detect?
- What can camera actually detect?
- What can LiDAR actually detect?
- What can thermal detect?
- What does GPS actually do?
- Why is sensor fusion required?
- What exactly does AI do?
- What exactly does the software decide?
- What exactly does the hardware do?

## 70. Tier 2 — MUST DESIGN
- System architecture
- Sensor selection
- Processing hardware
- Communication architecture
- Driver interface
- Dashboard
- Risk calculation
- AI model
- Dataset
- Prototype
- Testing environment
- Evaluation metrics

## 71. Tier 3 — MUST VALIDATE
- Cost
- Power
- Network
- Weather
- Dust
- Rain
- Fog
- vibration
- temperature
- false positives
- false negatives
- sensor failure
- communication failure
- AI failure

## 72. Tier 4 — WINNING PRESENTATION
- Strong problem story
- Real statistics
- Real incidents
- Primary sources
- Existing solution comparison
- Clear gap
- Clear innovation
- Working prototype
- Live demo
- Measured results
- Cost
- Deployment plan
- Business model
- Scalability
- Safety/fail-safe design
- Future roadmap

## 73. What the Project Should NOT Do
This is equally important.

❌ The project should not state:
“The system uses AI, LiDAR, radar, thermal, GPS, blockchain, IoT and digital twins.”
That's technology soup.

Instead:
“The driver loses situational awareness in dense fog. Radar provides robust object ranging, the camera provides object classification, GPS/map data provides road context, and the software combines these inputs to estimate collision risk and issue an actionable warning.”
Every technology must have a job.

## 74. Avoid the Quadruped Problem Mistake
The railway PS has a huge scope:

quadruped
handheld
narcotics
explosives
facial recognition
thermal
LiDAR
surveillance
GPS
control room
offline operation
etc.
The mining PS also lists many technologies.
That does not mean that all of them are expected to be built.
The correct question is:

“What is the smallest complete system that genuinely solves the central problem?”

## 75. Initial Possible MVP
An initial investigation could consider the following MVP:

              MINE VEHICLE

        ┌─────────────────────┐
        │                     │
        │      CAMERA         │
        │         ↓           │
        │      RADAR          │
        │         ↓           │
        │    GPS + IMU        │
        │         ↓           │
        │  EDGE COMPUTER      │
        │         ↓           │
        │  SENSOR FUSION      │
        │         ↓           │
        │ COLLISION RISK      │
        │         ↓           │
        │ DRIVER ALERT        │
        │                     │
        └─────────────────────┘
                  │
                  ↓
           CONTROL ROOM
This is not necessarily the final solution.
It provides the team with a starting hypothesis to test.

## 76. Required Research Question
The following exact question should appear at the top of the research document:

“How can a mine-dumper operator be provided with reliable information about nearby hazards, vehicle movement and road conditions when human visibility becomes insufficient, without making the system too expensive or unreliable for real mine deployment?”
If the team can answer that question, it is beginning to understand the PS.

## 77. Division of Research Among 6 People
Given a six-person team, research should be divided rather than assigned identically to every member.

Person 1 — Mining Domain
Research:

NMDC
Bailadila
mining operations
HEMM
haul roads
vehicle movement
monsoon/fog
Deliverable: “How the mine actually works.”

Person 2 — Accident & Safety
Research:

DGMS
accident statistics
accident cases
causes
regulations
existing safety procedures
Deliverable: “Why this problem matters.”
DGMS should be one of this person's primary sources. Its published material specifically documents serious dumper/tipper/truck accident patterns and safety interventions. (Directorate General of Mines Safety)

Person 3 — Sensors
Research:

radar
camera
LiDAR
thermal
GPS
IMU
Deliverable:

“Which sensor should be used and why?”

Person 4 — AI/Software
Research:

object detection
tracking
sensor fusion
collision prediction
datasets
edge AI
Deliverable:

“What exactly will our AI/software do?”

Person 5 — Hardware/Prototype
Research:

Jetson/Raspberry Pi/etc.
sensors
power
communication
mounting
fog simulation
BOM
Deliverable:

“Can this actually be built?”

Person 6 — Existing Solutions + Business
Research:

existing mining systems
competitors
cost
deployment
business model
scalability
market
procurement
Deliverable:

“Why would NMDC actually use/buy this?”

## 78. Consolidation of Research
After all research is completed, one master document should be created:

1. Problem
       ↓
2. Evidence
       ↓
3. Root causes
       ↓
4. Existing solutions
       ↓
5. Existing gaps
       ↓
6. Design requirements
       ↓
7. Proposed solution
       ↓
8. Hardware
       ↓
9. Software
       ↓
10. AI
       ↓
11. Sensor fusion
       ↓
12. Communication
       ↓
13. Prototype
       ↓
14. Testing
       ↓
15. Results
       ↓
16. Cost
       ↓
17. Deployment
       ↓
18. Business model
       ↓
19. Scalability
       ↓
20. Impact

## 79. The “Commit or Do Not Commit” Test
Before SIH26007 is officially selected, the team should be able to answer these 15 questions without external searching during the discussion:

What exactly is the danger caused by fog?
Who is in danger?
What type of accidents can occur?
Why are existing safety systems insufficient?
What does the driver need to know?
Which sensor provides that information?
Why is radar useful?
Why is camera useful?
Why might LiDAR fail in dense fog?
Why might thermal imaging produce false detections?
What exactly does AI do?
What exactly does the non-AI software do?
What happens if the system is wrong?
How will it be demonstrated?
Why would NMDC actually deploy it?
If the team can confidently answer all 15:

🟢 The problem is understood sufficiently to start designing.
If the team can answer only 5–6:

🟡 Keep researching.
If the team is still saying:

“AI + LiDAR + radar will be used because the problem statement mentions them.”
🔴 Do not commit yet.

## 80. One Important Consideration
An earlier observation was:

“This problem seems too generic.”
After careful examination, the underlying problem is not generic.
The generic version is:

“AI-based collision detection for vehicles.”
That is boring.
The interesting version is:

“How can safe, productive movement of extremely large mine haul vehicles be maintained when the operator's human visibility collapses to only a few metres during severe monsoon fog?”
The resulting scope includes:
Mining + extreme weather + heavy machinery + human safety + sensor fusion + edge computing + fleet coordination + productivity + real-world deployment.
This is considerably more specific.
And there is real evidence that heavy vehicle transportation is a major safety concern in open-cast mining: DGMS has repeatedly issued interventions around dumpers, trucks and other wheeled trackless transportation machinery, including collision, reversing, rear-vision and HEMM safety measures. (Directorate General of Mines Safety)

## 81. Immediate Next Step
Sensors should not yet be purchased.
The following activities should be completed first:

Phase 1 — Understand the mine
- Understand Bailadila.
- Understand HEMM.
- Understand haul roads.
- Understand dumper operation.
- Understand monsoon conditions.

Phase 2 — Prove the problem
- Collect accident data.
- Collect real incidents.
- Collect visibility/weather information.
- Quantify operational losses.
- Identify current safety mechanisms.

Phase 3 — Understand technology
- Camera
- Radar
- LiDAR
- Thermal
- GPS
- IMU
- Sensor fusion
- V2V
- V2I

Phase 4 — Define the intelligence
- What does the system detect?
- What does AI classify?
- What does software calculate?
- What does the system predict?
- What warning does the driver receive?

Phase 5 — Design
- Architecture
- Hardware
- Software
- AI
- Communication
- Dashboard

Phase 6 — Prototype
- Build small-scale environment.
- Simulate fog.
- Test sensors.
- Test detection.
- Test collision warning.
- Measure performance.

Phase 7 — Validate
- Accuracy
- latency
- range
- false alarms
- missed detections
- cost
- power
[communication

Phase 8 — Winning Story
- Problem
- Evidence
- Gap
- Solution
- Innovation
- Demo
- Results
- Cost
- Deployment
- Business
- Impact

Final takeaway
The first milestone for the team should not be a prototype.
The first milestone should be:

“Every member of our six-person team can explain the problem, the danger, the existing solutions, the technological gap, and exactly what our proposed system is supposed to sense, understand, predict, and communicate.”
Once that point is reached, the actual solution can be designed from the ground up — sensor by sensor, hardware by hardware, AI model by AI model, software module by software module, and finally the physical prototype and presentation.
The research should begin with DGMS + NMDC primary documents rather than random blogs. NMDC publishes its annual reports, and DGMS provides accident statistics, circulars and safety material. (National Marine Data Center)
Importantly, the project should not attempt to prove that the system will “eliminate accidents.” The scientifically defensible goal is to improve situational awareness, reduce collision risk, and provide earlier/more reliable warnings under low visibility. That distinction will make the team sound much more credible to judges.
