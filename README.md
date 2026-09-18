# Smart India Hackathon Workshop
# Date:18/09/2026
## Register Number:212225240105
## Name:Ponsriram P
## Problem Title
SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations
## Problem Description
Background: Railway stations are complex environments with numerous facilities and locations such as ticket counters, platforms, restrooms, food courts, and waiting areas. Passengers often face difficulties in navigating these spaces, especially in large or unfamiliar stations. Efficient and user-friendly navigation systems are crucial for improving passenger experience, reducing congestion, and ensuring timely travel connections. Description: The problem involves developing a comprehensive navigation solution for railway stations that assists passengers in locating various facilities and destinations within the station premises. This includes creating detailed maps, providing real-time directions, and integrating features such as accessibility options for individuals with disabilities. The solution should be intuitive, easy to use, and accessible via multiple platforms, including mobile devices and digital kiosks. Key challenges include updating navigation information in real-time, ensuring accuracy, and accommodating the diverse needs of all passengers. Expected Solution: The expected solution is a multi-platform navigation system that provides detailed, real-time directions to all facilities and locations within a railway station. This system should include: A mobile application with 3D interactive maps and step-by-step navigation. Digital kiosks located throughout the station with touch-screen interfaces. Voice-guided navigation for visually impaired passengers. Regular updates to reflect changes in station layout and facility locations. Integration with existing railway apps and services for seamless user experience. The solution should enhance the overall passenger experience by reducing confusion, saving time, and improving accessibility within the station.

## Problem Creater's Organization
Ministry of Railway

## Idea
### RailNavi
RailNavi treats time-to-departure as the primary input to every route — not an afterthought bolted onto a generic indoor map. Facility-finding (restrooms, food courts, ATMs, waiting areas) remains a full first-class mode, but journey-critical navigation leads.

| Common approach in this space | RailNavi |
|---|---|
| 3D / AR interactive maps | Lightweight 2D vector maps — loads in under 2 seconds on a budget Android phone, works over poor station Wi-Fi |
| Dense BLE beacon network across every station (high install + battery/maintenance cost, hard to scale to 7,000+ Indian stations) | Beacon-free: sparse QR/NFC anchors only at decision points + Wi-Fi RSSI fingerprinting off existing station Wi-Fi + on-device dead reckoning |
| Static point-to-point routing ("find the restroom") | Routing that is aware of your specific train's live ETA and platform, and silently recalculates if either changes |
| Voice guidance as a single accessibility add-on | Voice and distinct haptic vibration patterns as equal, independent channels |
| One generic "accessibility mode" toggle | Separate routing graphs for stairs / escalators / ramps / lifts, so a wheelchair or trolley route is physically valid — not just narrated |
| A native app the passenger must find and install | A Progressive Web App opened instantly via QR/NFC at any gate or kiosk — zero install |
| Map updates require a new app release or manual redeploy | A staff-editable digital twin — layout or platform changes go live on every phone and kiosk within seconds |

### Core Idea
 
#### 1 Time-Critical Routing
When a passenger scans their ticket QR or enters their PNR, RailNavi doesn't just draw a path — it surfaces platform number, live delay/ETA, walking time via the least congested route, and a countdown buffer. If the platform changes mid-walk (common at busy junctions), the route recalculates automatically with a single, calm voice/haptic alert: "Platform changed to 6. Recalculating your route."

#### 2 Beacon-Free Positioning
A full BLE beacon rollout costs lakhs per station and needs ongoing battery swaps and maintenance — a large part of why "real-time accuracy" and station-wide coverage stay open challenges in this brief. RailNavi fuses three inexpensive signals instead:

Static QR/NFC anchors (printed stickers, no power source) placed only at decision points — staircases, junctions, gates.
Wi-Fi RSSI fingerprinting against the free station Wi-Fi access points already installed at most stations under RailWire — no new hardware.
On-device dead reckoning — phone accelerometer step-counting plus compass heading — to interpolate position between anchors.
A lightweight Kalman filter fuses the three into one position estimate, re-anchored every time the passenger passes a QR/NFC point. Resolution is coarser than dense BLE (roughly 3–5 m instead of 1–2 m), which is a deliberate trade-off: good enough for corridor-level guidance, at close to zero incremental hardware cost per station.

#### 3 Crowd-Aware Routing
Anonymized Wi-Fi probe-request density per corridor (already broadcast passively by nearby phones) builds a live congestion heatmap. When time allows, routing prefers the less-congested corridor, and it actively steers passengers away from the worst choke points right after a platform change — directly targeting the brief's own goal of "reducing congestion," rather than treating navigation and crowd safety as separate problems.

#### 4 Accessibility as a Routing Graph, Not a Toggle
Most proposals bolt on "voice-guided navigation for the visually impaired" as a single checkbox. RailNavi instead keeps separate edge weights in the underlying routing graph for stairs, escalators, ramps, and lifts, so a wheelchair user or someone with a heavy trolley gets a path that is physically usable — never routed up a staircase because an escalator icon happened to look fine on a generic map. Voice guidance is paired with distinct phone-vibration patterns (short-short for "turn left," one long pulse for "turn right," rapid pulses for "arrived") so passengers in loud environments, or with combined vision/hearing difficulty, still get a directional cue.

#### 5 Zero-Install Adoption
RailNavi ships as a single Progressive Web App. A QR/NFC tap at any station gate, ticket counter, or kiosk opens it instantly in the phone's browser — no app-store install, no storage worry on budget phones. The exact same PWA runs in kiosk mode on station touchscreens, so passengers, station staff, and kiosks all read from one live "digital twin" instead of three systems slowly drifting out of sync.

#### 6 Live-Editable Digital Twin
A simple staff CMS, used by the station master's office, lets staff mark a blocked corridor, a platform change, or a temporary stall in under a minute. The change is live on every phone and kiosk immediately — no app redeployment, no waiting for the next map release. This is a direct answer to the brief's own flagged challenge of "updating navigation information in real time."
## Proposed Solution / Architecture Diagram

<img width="1494" height="481" alt="image" src="https://github.com/user-attachments/assets/246fb417-2688-466b-a636-76b53978f570" />

## Use Cases


## Technology Stack
| Layer | Technology | Why |
|---|---|---|
| Client | React + Vite PWA, 2D Canvas/Leaflet renderer | Fast load on low-end phones; works offline via service worker; avoids the slow-loading 3D/WebGL problem that sinks many rival proposals |
| Positioning | TensorFlow Lite on-device fingerprint matcher, optional Web Bluetooth fallback | Runs entirely on-device; beacon support only where a station already has them |
| Routing | Node.js/Express, custom A*/Dijkstra graph engine | Fast recomputation on live ETA or crowd changes |
| Real-time data | Adapter for an NTES/PRS-style live train feed (simulated feed for the prototype, pending official Railways API access), Redis for live cache | Keeps the demo unblocked while integration is pursued |
| Database | PostgreSQL + PostGIS | Spatial station graph, per-station editable |
| Staff CMS | React admin panel, role-based access | Lets station staff push layout/closure updates instantly |
| Voice / Haptic | Web Speech API with bundled offline TTS per station, Vibration API | Works without connectivity in basement/underground zones |

## Dependencies
