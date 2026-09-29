+ Zackary Santos
+ Last Saved: 9/29/2026 3:23 PM
+ Challenge #6 - Starbase7 Bug Fix Hunt
+ Solved some bugs so the code works
+ Reviewer Name: Valery Lot
+ Review: Still some bugs, we aren't getting the results we are expecting. I've listed them below.

Ships: 06 PUT /api/ships/2/refuel results in a 200 status code, should be 204 status code.

Pilots: 20 GET /api/pilots/3 doesn't result in 100 flight hours.
26 GET /api/pilots/total-hours results in 1555 hours. 