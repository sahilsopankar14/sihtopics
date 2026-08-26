SIH26007 — Pre-Commitment Research Report
Safe and Efficient Operation of Mine Vehicles in Fog and Low-Visibility Conditions in Open Cast Iron Ore Mines
Problem Statement: SIH26007
Ministry: Ministry of Steel
Organization: NMDC
Category: Hardware / Smart Automation
Core domain: Mining safety + intelligent transportation + sensor fusion + AI/ML + IoT + driver assistance

1. First: What exactly is the problem?
Before thinking about LiDAR, radar, AI, cameras, dashboards, etc., understand this one sentence:

A huge mining vehicle has to travel on a mine haul road, but during severe fog its driver cannot see far enough ahead to safely operate the vehicle at normal/efficient speeds.
The problem is therefore not simply “fog.”
The real problem is:
Low visibility → reduced situational awareness → increased uncertainty → driver slows/stops or may fail to detect hazards → collision/accident risk increases → haulage efficiency decreases → production is affected.
The official problem statement says Bailadila can experience visibility as low as 3–5 metres during severe monsoon conditions. (SIH Fit)
Imagine this:

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
The driver may simply not have enough information to make a safe decision.

2. What can actually go wrong?
This is one of the most important things your entire team needs to understand.
Don't say only:

“Fog causes accidents.”
Understand how the accident happens.

Scenario A — Vehicle ahead
Your dumper
     ↓
   🚛  ───────────────→

              🚛
        Vehicle ahead
Your vehicle is travelling at, say, 20–25 km/h.
Because of fog:

driver cannot see far ahead
another dumper is moving/stopped
driver notices it too late
braking distance is not enough
collision occurs
Your system should therefore answer:
“Is there an object/vehicle ahead, how far away is it, how fast is it moving, and is the current situation dangerous?”

3. Scenario B — Human/person ahead
Imagine a worker crossing the haul road.

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

4. Why do we need AI?
This was one of your biggest questions, and you're absolutely right to ask it.
You don't need AI just because the SIH problem statement says AI/ML.
Consider a simple radar.
Radar says:

Object detected at 30 m.
That's already useful.
You could write:

IF object_distance < 20m
    THEN WARNING
No AI required.
But now imagine:

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
“How confident are we?”
“What is the likelihood of collision?”
That is where AI becomes meaningful.

5. Very important distinction
Your system has three different jobs.
Don't mix them together.

Job 1 — SENSING
Hardware asks:

“What is physically around me?”
Examples:

radar
LiDAR
camera
thermal camera
GPS
IMU

Job 2 — PERCEPTION / INTERPRETATION
Software/AI asks:

“What am I looking at?”
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

Job 3 — DECISION
Software asks:

“What should I do about it?”
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
That is the core architecture you were trying to understand.

6. What is the actual solution we are imagining?
At this stage, do not commit to the exact hardware yet.
But a possible architecture could look like:

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
This is much more meaningful than saying:

“We'll use AI + LiDAR + IoT + GPS.”

7. What exactly should the system monitor?
This is another question you need to answer before building.
Your monitoring system could monitor:

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

8. What should the driver actually see?
This is extremely important.
Do not make the driver look at a complicated dashboard while driving a giant dumper.
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
The driver shouldn't need to interpret charts.

9. What is the control-room dashboard?
Think of it as air-traffic control for mine vehicles.
Instead of monitoring airplanes, the operator monitors dumpers.
Something like:

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

10. What does the AI model actually predict?
This needs to be one of your research questions.
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
But do not assume every one of these belongs in your final prototype.

11. What does LiDAR mean?
You specifically asked about this.
LiDAR = Light Detection and Ranging.
Think of it as a sensor that uses laser/light pulses to measure distances.
Imagine throwing thousands of tiny invisible measuring tapes around the vehicle.

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
 . . . . . .
.     🚛     .
 . . . . . .
Thousands/millions of points can describe:

road
vehicle
wall
rock
terrain
obstacles
That's what we meant by a 3D shape/map.

12. But LiDAR has a problem
LiDAR uses light.
Fog contains water droplets.
Rain contains water droplets.
Dust contains particles.
Those particles can scatter/reflect the laser.
Therefore:

Heavy fog, rain and dust can degrade LiDAR performance.
This is why you shouldn't simply say:

“We'll use LiDAR because it's accurate.”
You should ask:

“How does LiDAR behave in Bailadila's actual environmental conditions?”
That's a research question.

13. What is radar?
Radar uses radio waves rather than visible light.
Think of it like:

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
That's where another sensor can complement it.

14. Camera
Camera = your system's eyes.
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

15. Thermal camera
Thermal camera detects infrared radiation associated with temperature.
So:

Normal camera:
"What does it look like?"

Thermal:
"What temperature/heat pattern does it emit?"
A human may stand out from the background.
But you correctly identified an important problem:

Hot machinery and hot rocks can also produce strong thermal signatures.
Therefore:
thermal ≠ automatic human detection.
It needs interpretation and/or sensor fusion.

16. GPS
GPS answers:

“Where am I?”
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

17. GPS + mapping
Now it becomes more interesting.
Suppose the system knows:

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

18. What is V2V?
V2V = Vehicle-to-Vehicle communication.
Imagine two dumpers:

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
This is powerful in fog because the vehicles don't have to depend entirely on visual detection.

19. What is V2I?
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

20. The biggest concept you need to research: Sensor Fusion
I think this is one of the concepts you were missing.
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
This is potentially the core technical direction of your project.

21. What is the core engineering problem?
Don't define your project as:

“We are making an AI system for mines.”
That's weak.
A stronger definition is:

“We are developing a multi-sensor driver-assistance and fleet-awareness system that maintains situational awareness of mine vehicles when human visibility becomes inadequate.”
Now everything has a purpose.

22. Research Checklist — BEFORE COMMITTING
This is the most important section.
Don't start hardware development until your team has checked these.
A. Problem Understanding
 Can every team member explain the problem in their own words?
 Can everyone explain why fog is dangerous?
 Can everyone explain what happens when visibility drops to 3–5 m?
 Understand what HEMM means.
 Understand what a haul road is.
 Understand what a dumper is.
 Understand the typical mine transportation cycle.
 Understand loading → transportation → unloading → return.
 Understand why stopping vehicles affects production.
 Understand the difference between safety and productivity.
 Identify exactly what the driver cannot see.
 Identify exactly what information the driver needs.
 Identify exactly what decisions the driver has to make.

23. Mining Operations Research
 Learn how open-cast iron ore mining works.
 Study Bailadila mines.
 Study Kirandul.
 Study Bacheli.
 Study Donimalai.
 Understand mine haul roads.
 Understand mine road geometry.
 Understand gradients.
 Understand curves/hairpin bends.
 Understand loading points.
 Understand dumping/unloading points.
 Understand mine traffic rules.
 Understand HEMM.
 Understand dumper sizes.
 Understand typical dumper speeds.
 Understand braking distances.
 Understand blind spots.
 Understand reversing.
 Understand overtaking.
 Understand mixed traffic.
 Understand interaction between light vehicles and heavy vehicles.
DGMS material is particularly important here because vehicle movement is a recognized safety issue in open-cast mining. DGMS has specifically highlighted wheeled trackless transportation machinery, including dumpers and trucks, and historical guidance has emphasized visibility, haul roads and vehicle safety. (Directorate General of Mines Safety)

24. Accident Research
This should be one of your highest-priority research tracks.
Don't search only for:

“fog mining accidents.”
Search broadly for:

 Indian open-cast mine accidents
 dumper accidents
 HEMM accidents
 haul-road accidents
 vehicle collision accidents
 run-over accidents
 reversing accidents
 head-on collisions
 vehicle rollover
 blind-spot accidents
 visibility-related accidents
 monsoon mining accidents
 Bailadila accidents
 NMDC safety incidents
 DGMS accident statistics
A particularly useful official source is the DGMS annual report. Its 2024 report states that 36% of fatal accidents analyzed in 2023 in opencast coal mines involved dumpers, tippers, trucks and similar vehicles; among those accidents, it reports run-over, being-hit, head-on collision and toppling categories. (Directorate General of Mines Safety)
Important: Don't present this as “36% of all Indian mining accidents.” It is specifically the DGMS analysis described in that report. Always preserve the source context.

25. Accident Data Table
Build your own research spreadsheet.

| Year | Mine | Vehicle | Accident type | Cause | Visibility/weather | Fatalities | Injuries | Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| YYYY | Mine | Dumper | Collision | Visibility | Fog | XX | XX | DGMS |
| YYYY | Mine | Dumper | Run-over | Human/vehicle | Unknown | XX | XX | DGMS |

Try to build 20–50 credible incidents.
Then look for patterns.
You want to be able to say:

“We didn't invent this problem. We analyzed actual incidents and found recurring failure modes.”

26. Research the Existing Safety Systems
You need to know:

“What are mines already doing?”
Otherwise a judge can ask:

“Why isn't the existing system enough?”
Research:

 Rear-view cameras
 Reverse alarms
 Proximity detection
 Collision avoidance systems
 Operator training
 Mine traffic rules
 Speed monitoring
 Fleet management
 GPS tracking
 Radio communication
 Lighting systems
 Fog lights
 Beacon systems
 Radar systems
 Camera systems
 Driver monitoring
 Dispatch systems
DGMS records show that safety provisions already exist around HEMM, rear vision, alarms, haul roads and transportation. That means your solution needs to complement or improve existing controls, not pretend nothing exists. (Directorate General of Mines Safety)

27. Competitor / Existing Technology Research
Find commercial systems.
Research:

 Mining collision avoidance systems
 Mining proximity detection systems
 Autonomous haul trucks
 Radar-based collision warning
 LiDAR mining systems
 Thermal mining systems
 Mine fleet management
 ADAS for heavy vehicles
 V2V mining systems
 Open-pit mine safety systems
For every system record:

Company
Product
Sensors
Features
Price if available
Deployment environment
Strengths
Weaknesses
What it doesn't solve
Your goal is to find:

The gap.

28. Sensor Research
Create a separate document.

Camera
Research:

 RGB camera
 low-light camera
 night vision
 camera resolution
 FPS
 field of view
 fog performance
 rain performance
 dust performance

Radar
Research:

 What radar actually measures
 radar frequency bands
 detection range
 angle resolution
 velocity measurement
 fog performance
 rain performance
 dust performance
 false detections
 cost
 availability

LiDAR
Research:

 How LiDAR works
 point cloud
 2D vs 3D LiDAR
 range
 accuracy
 field of view
 fog limitations
 rain limitations
 dust limitations
 computational requirements
 cost

Thermal
Research:

 Thermal imaging basics
 human detection
 machinery detection
 hot rocks
 temperature differences
 rain/fog effects
 thermal resolution
 cost

GPS/DGPS
Research:

 GPS accuracy
 DGPS accuracy
 RTK GPS
 GPS limitations
 GPS-denied environments
 vehicle tracking
 geofencing
 digital maps

IMU
Learn:

 accelerometer
 gyroscope
 orientation
 vehicle motion
 sensor fusion with GPS

29. Sensor Comparison Matrix
You should eventually create something like:

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

Don't blindly copy these ratings into your final presentation. Validate them experimentally and from manufacturer/technical documentation.

30. Sensor Fusion Research
This should be a major research topic.
Learn:

 What sensor fusion means
 Early fusion
 Late fusion
 radar + camera fusion
 LiDAR + camera fusion
 GPS + IMU fusion
 Kalman filtering
 object tracking
 multi-object tracking
 confidence scores
 false positives
 false negatives

31. AI/ML Research
Don't just learn “AI.”
Determine exactly where AI is useful.
Research:

 Object detection
 YOLO
 object classification
 object tracking
 semantic segmentation
 road segmentation
 obstacle detection
 anomaly detection
 collision prediction
 time-to-collision
 sensor fusion ML
 edge AI
 model latency
 model accuracy
 false-positive rate
 false-negative rate

32. The Most Important AI Question
Ask:

“What prediction does our AI make that a simple threshold/rule cannot make reliably?”
If you can't answer that, don't use AI there.
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
That distinction will make your project much more technically credible.

33. Collision Prediction Research
This is potentially one of the most important areas.
Research:

 stopping distance
 reaction time
 braking distance
 vehicle speed
 relative velocity
 distance
 time-to-collision (TTC)
 trajectory prediction
 road geometry
 vehicle heading
For example:

Vehicle speed = 25 km/h
Distance = 15 m
Object speed = 0
The system needs to determine:

“Is 15 m safe or dangerous?”
Distance alone isn't enough.

34. Road-Curve Detection
You specifically asked about this.
Research three approaches:

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
Then compare them.

35. Communication Research
Research:

 Wi-Fi
 LoRa
 private LTE/5G
 RF communication
 V2V
 V2I
 MQTT
 CAN bus
 Ethernet
 edge-to-cloud communication
 offline operation
 communication latency
 packet loss
 communication range

36. Hardware Research
You need to determine:

Processing
Possible platforms:

 Raspberry Pi
 NVIDIA Jetson
 ESP32
 Arduino
 STM32
 industrial edge computer

Sensors
 radar
 camera
 GPS
 IMU
 optional LiDAR
 optional thermal

Driver interface
 display
 buzzer
 vibration
 LEDs
 speaker

Communication
 wireless module
 networking
 control-room connection

37. Software Research
Your software team should investigate:

Edge software
 sensor data acquisition
 preprocessing
 object detection
 object tracking
 sensor fusion
 risk calculation
 alert generation

Backend
 API
 database
 event storage
 vehicle telemetry
 user management

Dashboard
 live map
 vehicle positions
 active alerts
 historical incidents
 vehicle status
 weather/visibility
 analytics

AI
 model training
 dataset
 model deployment
 inference
 edge optimization

38. Dataset Research
This could become one of your biggest challenges.
Ask:

Where are we getting training data?
Research:

 mining vehicle datasets
 fog datasets
 pedestrian detection datasets
 vehicle detection datasets
 adverse weather datasets
 synthetic fog generation
 custom dataset collection
 simulation
 data augmentation
You may discover that actual Indian mine fog datasets are difficult to obtain.
That itself becomes a major project consideration.

39. Prototype Research
Before buying components, decide:

What exactly are we demonstrating?
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
Then demonstrate:

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

40. Fog Simulation Research
Your real environment is difficult to reproduce.
Research:

 fog chamber
 ultrasonic fogger
 water mist
 controlled visibility
 visibility measurement
 camera degradation
 radar performance
 LiDAR performance
The goal is not:

“Look, we added smoke.”
The goal is:

“At controlled visibility levels, we measured how our system behaves.”
That is much stronger.

41. Testing Metrics
Judges will appreciate measurable results.
Research how to measure:

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

42. Cost Research
This is extremely important because the PS specifically asks for a cost-effective solution.
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

Then ask:

Could a mine realistically deploy this on 10, 100 or 500 vehicles?
That's where your project becomes commercially interesting.

43. Ruggedization Research
Remember:
You aren't building this for a college laboratory.
You're building for:

rain
mud
dust
vibration
heat
humidity
mechanical shocks
long operating hours
Research:

 IP ratings
 vibration resistance
 temperature range
 waterproofing
 dust protection
 mounting
 cable protection
 sensor cleaning
 maintenance

44. Power Research
Research:

 vehicle power supply
 voltage conversion
 power consumption
 battery backup
 surge protection
 thermal management
 emergency shutdown

45. Mine Connectivity Research
Do not assume:

“There will be Wi-Fi everywhere.”
Research actual mine communication conditions.
Ask:

 Is cellular available?
 Is 4G available?
 Is 5G available?
 Is Wi-Fi available?
 Is private network infrastructure available?
 Are there dead zones?
 Can the system work offline?
 What happens if communication fails?
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

46. Fail-Safe Research
This is a safety system, so failure matters.
Research:

 What happens if radar fails?
 What happens if camera fails?
 What happens if GPS fails?
 What happens if AI crashes?
 What happens if network fails?
 What happens if sensor gives incorrect data?
 What happens if power drops?
 What happens if system overheats?
Your solution should never create a new danger.
For example:

False alert → annoying.
But:

Missed human detection → potentially catastrophic.
Therefore research false negatives carefully.

47. Human Factors
The driver is not a robot.
Research:

 Driver workload
 alert fatigue
 too many warnings
 audible warning levels
 visual warning design
 vibration
 voice warnings
 reaction time
 usability
 training requirement
Ask:

What is the minimum information the driver needs to make the correct decision?

48. Regulatory Research
This is another area teams often forget.
Research:

 DGMS regulations
 Coal Mines Regulations where applicable
 metalliferous mine safety requirements
 HEMM safety requirements
 mine traffic rules
 vehicle safety standards
 radio/wireless regulations
 data privacy
 worker monitoring/privacy
 facial recognition implications if you ever include it
DGMS has specific safety provisions concerning HEMM and wheeled trackless transportation machinery, so regulatory compatibility needs to be part of your research. (Directorate General of Mines Safety)

49. Business Model Research
Yes — you should research this, but don't make it the center of a technical SIH presentation.
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

50. Deployment Model
Think about how your system goes from:

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

 Installation time
 Maintenance
 Calibration
 Training
 Network infrastructure
 Software updates
 Sensor replacement
 Scaling

51. Business Case
Don't only say:

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
Your business case becomes:

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

52. Sustainability
Research:

 fuel savings
 reduced idle time
 efficient haulage
 reduced accident-related waste
 energy consumption of electronics
 maintenance requirements

53. Scalability
Ask:

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
Research how your architecture scales.

54. Cybersecurity
Because you're creating connected vehicles, research:

 encrypted communication
 authentication
 secure device identity
 dashboard authentication
 firmware updates
 network security
 data integrity
 attack prevention
You don't want someone spoofing:

“Vehicle A is here”
when it isn't.

55. What Judges Will Probably Ask
Prepare answers to these.

Problem
Why is this actually a serious problem?
How frequently does it occur?
Who is affected?
How much does it cost?
What happens today?

Existing solutions
What is already being used?
Why isn't it sufficient?
What is your innovation?

Hardware
Why radar?
Why camera?
Why LiDAR?
Why thermal?
Why not only radar?

AI
Why AI?
What exactly does the model predict?
What dataset did you use?
What accuracy did you achieve?
What happens if the AI is wrong?

Safety
What happens if your system fails?
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
How will you install it?
What happens during maintenance?

56. What Your Presentation Should Eventually Contain
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
Don't claim existing systems are ineffective unless your research proves it.

57. Slide 5 — Your Solution
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

58. Slide 6 — How It Works
This is where your “automatic door” analogy becomes useful.

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

59. Slide 7 — AI
Don't say:

“We use AI.”
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

60. Slide 8 — Hardware
Show actual hardware.

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

61. Slide 9 — Software
Show:

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

62. Slide 10 — Control Room
Demonstrate:

live vehicle map
vehicle status
alerts
collision risk
visibility
historical events

63. Slide 11 — Prototype
This is where you impress the judges.
Don't pretend:

“We deployed it on a 240-ton dumper.”
Instead say:

“We created a scaled physical test environment representing the mine scenario.”
Then demonstrate:

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

64. Slide 12 — Results
This is crucial.
Don't only show screenshots.
Show:

Object detection accuracy: XX%
Detection range: XX m
Alert latency: XX ms
False alarm rate: XX%
Network latency: XX ms
Fog visibility tested: XX m
Actual measured numbers will make your presentation much stronger.

65. Slide 13 — Cost
Show:

Prototype cost
Deployment cost
Estimated per-vehicle cost
Maintenance

66. Slide 14 — Deployment
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

67. Slide 15 — Business Model
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

68. Slide 16 — Impact
Potential metrics:

reduced collision risk
improved driver awareness
reduced unnecessary stoppages
reduced cycle time
improved fleet utilization
improved monitoring
safer monsoon operations
Again: measure or calculate these from defensible assumptions. Don't manufacture percentages.

69. The Most Important Research Questions
If your team has limited time, answer these first.

Tier 1 — MUST KNOW
 What exactly happens during 3–5 m visibility?
 What are the actual accident mechanisms?
 How many relevant accidents occur?
 What does DGMS say?
 What safety systems already exist?
 What doesn't existing technology solve?
 What information does the driver need?
 Which sensors work in dense fog?
 What can radar actually detect?
 What can camera actually detect?
 What can LiDAR actually detect?
 What can thermal detect?
 What does GPS actually do?
 Why do we need sensor fusion?
 What exactly does AI do?
 What exactly does the software decide?
 What exactly does the hardware do?

70. Tier 2 — MUST DESIGN
 System architecture
 Sensor selection
 Processing hardware
 Communication architecture
 Driver interface
 Dashboard
 Risk calculation
 AI model
 Dataset
 Prototype
 Testing environment
 Evaluation metrics

71. Tier 3 — MUST VALIDATE
 Cost
 Power
 Network
 Weather
 Dust
 Rain
 Fog
 vibration
 temperature
 false positives
 false negatives
 sensor failure
 communication failure
 AI failure

72. Tier 4 — WINNING PRESENTATION
 Strong problem story
 Real statistics
 Real incidents
 Primary sources
 Existing solution comparison
 Clear gap
 Clear innovation
 Working prototype
 Live demo
 Measured results
 Cost
 Deployment plan
 Business model
 Scalability
 Safety/fail-safe design
 Future roadmap

73. What You Should NOT Do
This is equally important.

❌ Don't say:
“We use AI, LiDAR, radar, thermal, GPS, blockchain, IoT and digital twins.”
That's technology soup.

Instead:
“The driver loses situational awareness in dense fog. Radar provides robust object ranging, the camera provides object classification, GPS/map data provides road context, and the software combines these inputs to estimate collision risk and issue an actionable warning.”
Every technology must have a job.

74. Don't Make the Quadruped Problem Mistake
Your railway PS has a huge scope:

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
That doesn't mean you're expected to build all of them.
The correct question is:

“What is the smallest complete system that genuinely solves the central problem?”

75. Your First Possible MVP
If I were your technical mentor, I would initially investigate this:

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
Not because this is definitely the final solution.
Because it gives your team a starting hypothesis to test.

76. Your Team's Research Should Eventually Answer This
Put this exact question at the top of your research document:

“How can we provide a mine-dumper operator with reliable information about nearby hazards, vehicle movement and road conditions when human visibility becomes insufficient, without making the system too expensive or unreliable for real mine deployment?”
If your team can answer that question, you're starting to understand the PS.

77. Divide the Research Among 6 People
Since you have six people, I would not have everyone research everything.

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

“Which sensor should we use and why?”

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

“Can we actually build this?”

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

78. Then Combine Everything
After everyone finishes research, create one master document:

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

79. The “Commit or Don't Commit” Test
Before you officially choose SIH26007, I would want your team to be able to answer these 15 questions without Googling during the discussion:

What exactly is the danger caused by fog?
Who is in danger?
What type of accidents can occur?
Why aren't existing safety systems sufficient?
What does the driver need to know?
Which sensor provides that information?
Why is radar useful?
Why is camera useful?
Why might LiDAR fail in dense fog?
Why might thermal imaging produce false detections?
What exactly does AI do?
What exactly does the non-AI software do?
What happens if your system is wrong?
How will you demonstrate it?
Why would NMDC actually deploy it?
If your team can confidently answer all 15:

🟢 You understand the problem enough to start designing.
If you can answer only 5–6:

🟡 Keep researching.
If you're still saying:

“We'll use AI + LiDAR + radar because the problem statement mentions them.”
🔴 Don't commit yet.

80. One Important Thing I Want You to Remember
You said earlier:

“I feel this problem is too generic.”
After going through it carefully, I don't think the underlying problem is generic.
The generic version is:

“AI-based collision detection for vehicles.”
That is boring.
The interesting version is:

“How do you maintain safe, productive movement of extremely large mine haul vehicles when the operator's human visibility collapses to only a few metres during severe monsoon fog?”
Now you've got:
Mining + extreme weather + heavy machinery + human safety + sensor fusion + edge computing + fleet coordination + productivity + real-world deployment.
That's considerably more specific.
And there is real evidence that heavy vehicle transportation is a major safety concern in open-cast mining: DGMS has repeatedly issued interventions around dumpers, trucks and other wheeled trackless transportation machinery, including collision, reversing, rear-vision and HEMM safety measures. (Directorate General of Mines Safety)

81. Your Immediate Next Step
Do not buy sensors yet.
Do this first:

Phase 1 — Understand the mine
 Understand Bailadila.
 Understand HEMM.
 Understand haul roads.
 Understand dumper operation.
 Understand monsoon conditions.

Phase 2 — Prove the problem
 Collect accident data.
 Collect real incidents.
 Collect visibility/weather information.
 Quantify operational losses.
 Identify current safety mechanisms.

Phase 3 — Understand technology
 Camera
 Radar
 LiDAR
 Thermal
 GPS
 IMU
 Sensor fusion
 V2V
 V2I

Phase 4 — Define the intelligence
 What does the system detect?
 What does AI classify?
 What does software calculate?
 What does the system predict?
 What warning does the driver receive?

Phase 5 — Design
 Architecture
 Hardware
 Software
 AI
 Communication
 Dashboard

Phase 6 — Prototype
 Build small-scale environment.
 Simulate fog.
 Test sensors.
 Test detection.
 Test collision warning.
 Measure performance.

Phase 7 — Validate
 Accuracy
 latency
 range
 false alarms
 missed detections
 cost
 power
[communication

Phase 8 — Winning Story
 Problem
 Evidence
 Gap
 Solution
 Innovation
 Demo
 Results
 Cost
 Deployment
 Business
 Impact

Final takeaway
The first milestone for your team should not be a prototype.
Your first milestone should be:

“Every member of our six-person team can explain the problem, the danger, the existing solutions, the technological gap, and exactly what our proposed system is supposed to sense, understand, predict, and communicate.”
Once you reach that point, then we can sit down and design the actual solution from the ground up — sensor by sensor, hardware by hardware, AI model by AI model, software module by software module, and finally the physical prototype and presentation.
For your research, I would start with DGMS + NMDC primary documents, rather than random blogs. NMDC publishes its annual reports, and DGMS provides accident statistics, circulars and safety material. (National Marine Data Center)
And importantly, don't try to prove that your system will “eliminate accidents.” The scientifically defensible goal is to improve situational awareness, reduce collision risk, and provide earlier/more reliable warnings under low visibility. That distinction will make your team sound much more credible to judges.