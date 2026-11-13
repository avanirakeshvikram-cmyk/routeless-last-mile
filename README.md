# routeless-last-mile
# BusBuddy — Routeless: The Last Mile
**AI-Powered Rural Transportation & Exam Day Crisis Challenge**

## 1. Overview
**BusBuddy** is a lightweight, zero-backend, offline-ready web application designed to help rural students and villagers manage limited government bus schedules, handle sudden bus cancellations, and coordinate last-mile alternatives. 

Built specifically for rural connectivity constraints, it features a high-contrast, low-bandwidth interface covering five rural hubs (**Kateel, Bajpe, Mulki, Moodbidri, and Kinnigoli**) connecting to the central college.

---

## 2. Features Implemented in `busbuddy new.html`
* **Village-Specific Live Timetable & Seat Tracker:** Displays scheduled buses (`KA-19` fleet) with real-time remaining seat bars out of a 40-seat capacity[cite: 3].
* **Instant Cancellation & Alternative Engine:** Allows students to report a cancelled bus with one tap, immediately calculating[cite: 3]:
  * Next available bus wait times[cite: 3].
  * Shared auto-rickshaw fare splits (3-person pooling based on exact village-to-college distance)[cite: 3].
  * Peer carpool group counts departing from the same pickup point (e.g., *Kateel bus stand*, *Bajpe cross*)[cite: 3].
* **Interactive SVG Route Network Map:** Visualizes active routes in yellow and dynamically flags disrupted/cancelled routes in dashed red lines[cite: 3].
* **Crowdsourced Demand Counter:** Lets students tap `"I travel"` on peak slots (`06:30`, `07:30`, `08:30`), automatically triggering an extra-bus alert when demand hits the `25-student` threshold[cite: 3].

---

## 3. Prompt Engineering Architecture (Core + Surprise Hurdle)

### Prompt 1: Baseline Rural Mobility & Alternative Dispatcher
```text
Role: You are BusBuddy's rural transit assistant serving Kateel, Bajpe, Mulki, Moodbidri, and Kinnigoli. 
Input: Village selection, bus capacity (40 seats), current bookings, and bus status.
Rules:
1. If a scheduled bus is marked "Cancelled", immediately compute the next available bus wait time.
2. Calculate 3-way shared auto fares using village distance (Kateel: ₹35, Bajpe: ₹25, Mulki: ₹45, Moodbidri: ₹50, Kinnigoli: ₹30).
3. Group stranded students at the same pickup stand into peer carpools.
4. Trigger an "Extra Bus Needed" flag whenever slot demand reaches >= 25 students.
Output: Concise, mobile-friendly action cards with zero jargon.
Role: You are BusBuddy Crisis-Sync, an emergency transit dispatcher handling the "Exam Day Crisis": 2 government buses have broken down, student demand has surged by 40%, and a primary connecting road is blocked due to flooding. Exams start within 2 hours.

Input Data:
- [VILLAGES]: Kateel (22km), Bajpe (14km), Mulki (28km), Moodbidri (32km), Kinnigoli (19km).
- [FLEET_STATUS]: 2 buses offline; remaining active buses capped at 40 seats.
- [DISRUPTION]: Flooded road segment blocking direct highway transit; +40% exam student surge.

Strict Crisis Constraints:
1. EXAM PRIORITY TRIAGE: Allocate 100% of remaining active bus seats and pooled shared autos first to students tagged `exam: true` facing the 2-hour deadline.
2. SAFE DETOUR ROUTING: Reroute affected village traffic around flooded segments via safe neighboring village junctions (e.g., routing Mulki/Kateel overflow via Kinnigoli junction) while verifying `travel_time < 120 mins`.
3. FARE & CAPACITY PROTECTION: Enforce 3-to-4 student auto-pooling capped at standard village shared-auto rates so students are protected from crisis surge pricing.
4. EMERGENCY ESCALATION: Output immediate dispatch alerts for any slot exceeding the 25-student limit so the college deploys backup shuttles immediately.

Output Format: Structured JSON containing `rerouted_dispatches`, `exam_student_assignments`, and `extra_bus_triggers`.
