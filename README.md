# 📍 SPothole — AI-Based Pothole Complaint and Management System

> Software Engineering Final Project · University of Management and Technology (UMT)

A software design and planning project for a mobile + web system that lets citizens report potholes with a photo, verifies the photo using **Vision AI**, tags it with **GPS location**, and gives road authorities a **web dashboard** to track and resolve complaints.

This repository contains the complete project documentation: [`SE__FINAL_PROJECT.docx`](./SE__FINAL_PROJECT.docx).

![Cover](./images/cover.jpeg)

---

## 👥 Team

| Name | Student ID |
| --- | --- |
| Saif Ur Rehman Hashmi | F2024266593 |
| M. Saboor Arif | F2024266553 |
| Nauman Naseer | F2024266574 |

---

## 📌 Problem

Pothole reporting in many cities relies on manual complaints, phone calls, and physical inspections. This is slow, hard to follow up on, and authorities receive many **fake, duplicate, or unclear** reports that waste resources and delay repairs.

## 💡 Solution

A **Pothole Complaint Application**:

1. A citizen captures a pothole photo in the mobile app.
2. **Vision AI** checks that the image really contains a pothole. Fake images are rejected.
3. The app attaches **GPS coordinates** and the address.
4. The complaint is sent to the backend as **JSON** (image encoded as Base64).
5. Authorities view, manage, and update complaint status on a **web dashboard**.
6. The citizen gets notified when the status changes.

## 🎯 Objectives

- Simplify pothole reporting for citizens
- Use Vision AI to authenticate pothole images
- Identify pothole locations accurately with geolocation
- Give authorities a centralized complaint management system
- Improve road maintenance efficiency and public safety

## 🔭 Scope

| In scope | Out of scope |
| --- | --- |
| Mobile app for pothole reporting | Automatic pothole repair mechanisms |
| Image capture and upload | Integration with vehicle navigation systems |
| AI-based image validation | Real-time traffic rerouting |
| GPS-based location detection | |
| Backend server for complaint processing | |
| Web application for complaint management | |

**Stakeholders:** citizens (end users), municipal road maintenance authorities, system administrators, developers.

---

## 🔄 System Workflow

![System workflow](./images/workflow.jpeg)

The mobile app sends the captured image to Vision AI (Azure). If a pothole is detected, the image is Base64-encoded and sent with the address as a JSON payload to the backend web app, which stores it and displays it on the dashboard. If no pothole is detected, the user sees a "fake complaint" toast and is asked to retake the picture.

---

## 🧭 Development Model: Scrum (Agile)

Scrum was chosen because:

- **Requirements will change:** AI accuracy, complaint categories, and dashboard features will evolve.
- **Incremental delivery fits:** the system is built in small working sprints.
- **AI needs experimentation:** models need tuning, retraining, and gradual improvement.
- **User feedback is critical:** sprint reviews give formal feedback loops for usability and false positives.
- **Parallel development:** mobile, AI, and backend teams can work at the same time.

| Sprint | Deliverable |
| --- | --- |
| 1 | Basic mobile app + image upload |
| 2 | Geolocation tagging + JSON API |
| 3 | Vision AI pothole validation |
| 4 | Web dashboard for authorities |
| 5 | Optimization, security, analytics |

The document also explains why **Waterfall, V-Model, XP, Incremental, and Iterative** models were rejected, and why Scrum is preferred over the closest alternatives (Incremental and Iterative).

---

## ✅ Requirements

### Functional

- User registration and secure login
- Capture and upload pothole images
- Image validation using Vision AI
- Location detection and storage
- Complaint data sent to the backend as JSON
- Authority dashboard to view, manage, and update complaint status
- Duplicate check by coordinates, notifying users if a pothole is already reported
- Offline storage: save reports locally when there is no internet
- Fast processing: validation and upload within **10 seconds**
- Real-time feedback and notifications on complaint status

### Non-Functional

| Attribute | Requirement |
| --- | --- |
| Usability | Mobile app should be easy to use |
| Performance | Image validation within acceptable time limits |
| Reliability | Accurate complaint tracking |
| Security | User data and images securely stored |
| Scalability | Architecture allows adding more AI processing nodes as report volume grows |
| Interoperability | API endpoint exposing public "Confirmed Pothole" data to third-party navigation apps |
| Localization | Multi-language mobile interface |

---

## 🗓️ Project Plan (Gantt Chart)

![Gantt chart](./images/gantt-chart.png)

| Phase | Timeline |
| --- | --- |
| Requirement finalization & architecture | Jan – Feb |
| Core mobile app & GPS | Mar – Apr |
| Vision AI model training | Mar – Jun |
| Backend API & web dashboard | May – Aug |
| System integration & testing | Sep – Oct |
| Beta launch & user feedback | Sep – Oct |
| Final deployment & maintenance | Nov – Dec |

---

## 📐 Design Diagrams

### 1. Use Case Diagram
Actors: **User** (primary), **Authority**, **Vision AI System**, and **GPS Service** (secondary). *Submit Complaint* includes capturing/uploading the image, AI validation, location detection, and sending JSON; duplicate check, offline save, and notifications extend it.

![Use case diagram](./images/use-case-diagram.jpeg)

### 2. Entity-Relationship Diagram (ERD)
Entities: `User`, `Authority`, `Complaint`, `PotholeImage`, `Location`, `VisionAIValidation`, `ComplaintStatusHistory`, `Notification`, `OfflineReport`.

![ERD](./images/erd.jpeg)

### 3. Class Diagram
Core classes: `User`, `Authority`, `Complaint`, `Image`, `Location`, `Status`, `MobileApp`, `WebApp`, `BackendServer`, `VisionAIService`, `LocationService`, `DuplicateCheckService`, `OfflineStorage`, `Notification`.

![Class diagram](./images/class-diagram.jpeg)

### 4. Sequence Diagram
Covers four flows: user authentication, pothole reporting, complaint management, and notification.

![Sequence diagram](./images/sequence-diagram.jpeg)

### 5. Data Flow Diagram
Shows how data moves between the user, authority, processes (registration, upload, AI validation, duplicate check, status updates) and the user, complaint, notification, and local storage data stores.

![Data flow diagram](./images/data-flow-diagram.jpeg)

---

## 🧪 Test Cases

| ID | Scenario | Expected Result |
| --- | --- | --- |
| TC01 | Login with valid credentials | User logs in successfully |
| TC02 | Login with invalid password | "Invalid password" error shown |
| TC03 | Pothole detection with Vision AI | Image validated as a valid pothole |
| TC04 | Invalid image rejection (plain road, person) | "No Pothole Detected" error |
| TC05 | GPS location tagging | Latitude and longitude attached to complaint |
| TC06 | JSON data transmission | Data sent to server in valid JSON |
| TC07 | Admin complaint management | Status updated to "In Progress" and visible in database |
| TC08 | Offline data handling | "No Internet" message or complaint saved locally |
| TC09 | Image upload performance (5MB+) | Validation and upload within 10 seconds |
| TC10 | Duplicate complaint check | User notified the pothole is already reported |
| TC11 | User notification | Push notification when admin marks "Fixed" |
| TC12 | Multiple potholes in one frame | AI detects and marks all visible potholes |

---

## 🛠️ Tech Overview

| Layer | Technology |
| --- | --- |
| Mobile app | Camera, GPS/geolocation, offline local storage |
| AI | Vision AI (Azure Computer Vision) for pothole validation |
| Backend | JSON-based API, Base64 image transfer, database |
| Web dashboard | Complaint viewing, management, and status updates |

## 📂 Repository Contents

```
.
├── README.md
├── SE__FINAL_PROJECT.docx
└── images/
    ├── cover.jpeg
    ├── workflow.jpeg
    ├── gantt-chart.png
    ├── use-case-diagram.jpeg
    ├── erd.jpeg
    ├── class-diagram.jpeg
    ├── sequence-diagram.jpeg
    └── data-flow-diagram.jpeg
```

## 📄 License

Created for academic purposes at the University of Management and Technology.
