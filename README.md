# FoodConnect — To Supply Leftover Food To Poor

![FoodConnect](https://img.shields.io/badge/FoodConnect-%23FF6F00?style=for-the-badge&logo=foodpanda&logoColor=white)  
[![Platform: Salesforce](https://img.shields.io/badge/Platform-Salesforce-blue)](https://developer.salesforce.com/)  [![Status: Prototype](https://img.shields.io/badge/Status-Prototype-green)]

---

## 🚀 Project Title
FoodConnect — To Supply Leftover Food To People In Need  
A Salesforce-based Food Redistribution and Management System that collects surplus food from venues (restaurants, events, households) and delivers it safely to people in need using registered volunteers and drop-off points.

---

## 📘 Project Overview
Large volumes of edible food are discarded after events, restaurants, and canteens while vulnerable people remain hungry. FoodConnect centralizes donor and beneficiary data, automates pickup scheduling and volunteer routing, enforces food-safety checks, and provides transparent reporting — all built on Salesforce Lightning (Flows + Apex + Reports).

---

## 🎯 Objectives
- **Centralize** donor, pickup, volunteer, and drop-off point data.  
- **Automate** pickup creation and nearest-volunteer assignment.  
- **Ensure** food safety and traceability through handover records.  
- **Record** distribution details and collect beneficiary feedback.  
- **Implement** role-based secure access (Coordinator, Volunteer, Donor).  
- **Provide** real-time analytics via reports and dashboards.

---

## 🧩 System Architecture
### 🏗️ Entity Relationships
- Venue (Donor) → Pickup Request — One-to-Many  
- Pickup Request → Handover Record — One-to-One  
- Handover Record → Distribution Record — One-to-One  
- Drop-Off Point → Distribution Record — One-to-Many  
- Volunteer Team → Volunteer — One-to-Many  
- User Role → Users — One-to-Many

Each object enforces data integrity using validation rules, Flows, and Apex where transactional enforcement is required.

---

## ⚙️ Features
- Donor intake form with geolocation and acceptable food-type selection.  
- Auto-create Pickup Requests when venues report surplus.  
- Nearest-volunteer auto-assignment and shift management.  
- Handover record with temperature log, safety checklist, and signature capture.  
- Distribution logging with portions served and recipient feedback.  
- Email/SMS notifications for donors, volunteers, and coordinators.  
- Dashboards: meals delivered, safety incidents, volunteer utilization, geographic coverage.

---

## 🔒 Validation Rules
| Object | Rule (pseudo) | Error Message |
| --- | --- | --- |
| Pickup Request | Requested_Pickup_Date__c < TODAY() | You cannot request a pickup in the past. |
| Pickup Request | Estimated_Portions__c <= 0 | Enter a valid positive portion estimate. |
| Handover Record | Safety_Checklist__c = FALSE && Food_Temperature__c > 8 | Food must pass safety checks or be stored below 8°C. |
| Distribution Record | Portions_Distributed__c > Pickup_Request__r.Estimated_Portions__c | Distributed portions cannot exceed collected estimate. |

---

## 🔁 Automation
- Flows:
  - Auto-create Handover Record when Pickup Request status becomes "Collected".  
  - Auto-assign nearest available volunteer using geolocation and active shifts.  
  - Scheduled daily digest for Coordinators with pending pickups and safety alerts.
- Apex Trigger:
  - Prevent Distribution Record creation unless an approved Handover Record exists and timestamps are chronological.
  - Utility class for nearest-volunteer calculation (optional if complex geolocation logic needed).

---

## 👥 User Roles & Security
| Profile / Role | Access | Purpose |
| --- | --- | --- |
| Coordinator | Full CRUD on all entities + reports/dashboards | Oversee operations, manage volunteers and donors |
| Volunteer | Create/Edit assigned Handover & Distribution; Read limited | Handle pickups and deliveries |
| Donor Contact (Portal) | Create Pickup Requests; Read own records | Report surplus and view receipts |
| Drop-Off Manager | Read/Update Distribution Records | Manage on-site distribution and confirmations |

- Role Hierarchy: **Coordinator → Volunteer**  
- Sharing: Org-Wide Defaults = Private. Pickup/Handover/Distribution records shared with owning Volunteer Team and Coordinator role.

---

## 📊 Reports & Dashboards
| Report Name | Type | Key Filters | Purpose |
| --- | --- | --- | --- |
| Daily Pickup Summary | Summary | Pickup Date = Today | Track planned vs completed pickups |
| Meals Distributed by Area | Matrix | Distribution Date = Last 30 Days | Visualize geographic reach |
| Volunteer Utilization | Summary | Shift Date = Last 30 Days | Identify coverage gaps |
| Food Safety Exceptions | Tabular | Safety_Checklist = FALSE OR Temperature > 8 | Highlight safety incidents |

Dashboards: Impact Overview (KPI tiles), Coverage Map (heatmap), Volunteer Health, Safety & Compliance.

---

## 🧠 Tech Stack
| Layer | Technology |
| --- | --- |
| Platform | Salesforce Developer (CRM Cloud) |
| Logic | Flows (Screen, Record-Triggered, Scheduled) & Apex (triggers, utility classes) |
| Database | Salesforce Custom Objects (Venue, Pickup_Request, Handover_Record, Distribution_Record, Volunteer, Drop_Off_Point) |
| Notifications | Salesforce Email Alerts; optional SMS gateway integration |
| Analytics | Salesforce Reports & Dashboards; exportable datasets for BI tools |

---

## 🧑‍💻 Team
| Role | Name | Email |
| --- | --- | --- |
| Team Leader | Hariharan K | hariharankannan36@gmail.com |
| Team Member | Mukesh Raj | mukeshclg22site@gmail.com |
| Team Member | Punitha Kishore T | vinothkishore1817@gmail.com |
| Team Member | Arun Kumar S | arun0506kumar2005@gmail.com |

Team ID: **NM2025TMID02981**  
Institution: **P.S.R.R College Of Engineering — AI & DS Department**

---

## ✅ Implementation Checklis
1. Create custom objects: Venue, Drop_Off_Point__c, Volunteer__c, Pickup_Request__c, Handover_Record__c, Distribution_Record__c.  
2. Add essential fields:
   - geolocation (Latitude/Longitude)  
   - Estimated_Portions__c (Number)  
   - Food_Temperature__c (Number)  
   - Safety_Checklist__c (Checkbox)  
   - Status__c (Picklist: Requested, Assigned, Collected, Delivered, Completed)  
3. Build Flows:
   - Venue intake Screen Flow.  
   - Record-triggered Flow: create Pickup_Request on Venue surplus.  
   - Record-triggered Flow: auto-create Handover_Record when Pickup status = Collected.  
   - Scheduled Flow: daily coordinator digest.  
   - Screen Flow for Volunteer handover (temp, checklist, signature).  
4. Implement validation rules listed above.  
5. Write Apex trigger(s):
   - DistributionTrigger: enforce Handover existence and timestamp ordering.  
   - Optional: Geolocation utility class for nearest-volunteer logic.  
6. Configure Lightning App (FoodConnect) with navigation and Home page components.  
7. Setup Donor portal and Volunteer mobile-friendly Lightning pages.  
8. Create custom report types, reports, and dashboards.  
9. Pilot with 3 venues and 10 volunteers; gather feedback and iterate.

---

