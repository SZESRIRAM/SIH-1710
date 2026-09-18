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
# RailNavi
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
## Proposed Solution / Architecture Diagram


## Use Cases


## Technology Stack


## Dependencies
