# noticeBordDocumentation
# College Notice Board: Project Documents

Documentation set for the **College Online Notice Board System**, a role-based digital notice board built with **Spring Boot 3, React (Vite) and MySQL**.

It replaces the physical notice board. Staff create, approve, schedule and publish notices, each notice reaches only the audience its author chose, and visitors without an account see a public website.

This folder holds the explanations, diagrams and animations for the project. The source code lives in a separate folder (`college_notice_board/`, with `backend/` and `frontend/`).

---

## What is in this folder

| File | Type | What it is |
| --- | --- | --- |
| `Notice-Board-Project-Handbook.pdf` | PDF, 84 pages | The complete written reference: every page, class, table, endpoint and rule, plus viva questions, a presentation script and a demo script. |
| `College_Notice_Board_UML_Diagram_Set.html` | Interactive page | 17 UML, DFD and flow diagrams drawn with Mermaid. You can view the code, copy it, or download each diagram as SVG. |
| `College_Notice_Board_Animated_Project_Flow.html` | Interactive page | Six animated tabs that explain how the system works: architecture, registration, notice lifecycle, targeting, one request step by step, and scheduling. |
| `College_Notice_Board_Every_Role_Explained.html` | Interactive page | Role explorer, permission matrix, an all-roles story, and a tester that shows 401 and 403 responses. |
| `notice_board_flow.gif` | Animated GIF | The complete flow drawn step by step, one arrow at a time. |
| `notice_board_flow_arrows_only.gif` | Animated GIF | The same diagram with all boxes and text fixed. Only the arrows move. Best for slides. |

> The files may carry a numeric prefix from the upload (for example `1791785524804_...`). The names above are the clean versions, and you can rename them as you like.

---

## Where to start

Pick what you need:

| If you want to… | Open this |
| --- | --- |
| Understand the whole project quickly | `notice_board_flow_arrows_only.gif`, then the **Animated Project Flow** page |
| Know what each role can and cannot do | the **Every Role Explained** page |
| Show the design to a teacher or examiner | the **UML Diagram Set** page |
| Study every detail, or prepare for a viva | the **Project Handbook** PDF |
| Put the flow in a presentation | the two GIFs |

A good first reading order is:

1. `notice_board_flow_arrows_only.gif` gives the one-picture overview.
2. **Animated Project Flow** shows how it works.
3. **Every Role Explained** shows who does what.
4. **UML Diagram Set** gives the formal design.
5. **Project Handbook** has all the detail.

---

## How to open each file

- **HTML pages:** double-click the file to open it in a browser. They work offline except for web fonts, and the UML page needs an internet connection the first time because it loads Mermaid from a CDN (`cdn.jsdelivr.net`).
- **PDF:** any PDF reader.
- **GIFs:** any browser or image viewer, or drag them into PowerPoint or Google Slides. They loop forever.

---

## The project in one minute

```
Visitor ─► Register ─► Approver (auto-picked) ─► Login + JWT ─► Dashboard
                                                                    │
                                                              Create notice
                                                                    │
                                                             Choose audience
                                                                    │
                                                              Which role?
                                        ┌───────────────────────────┴───────────────┐
                                   Teacher                              HOD / Principal / Admin
                                      │                                             │
                               Submit to HOD ◄── rejected                    Publish directly
                                      │ approve                                     │
                                      └──────────────► PUBLISHED ◄──────────────────┘
                                                          │
                                         Members notified ─► Read + acknowledge ─► Expired / archived
```

**Key ideas**

- **The server decides who sees a notice.** Each notice has target rows (role, department, semester, class, or a person). A user sees the notice if any row matches. The rule is written once in Java and once in SQL, and tests check that they agree.
- **Nobody picks their own approver.** A student goes to the class teacher, then the HOD, then the Principal. A teacher goes to the HOD, then the Principal. An HOD goes to the Principal.
- **Teachers cannot publish directly.** Their notices go to the HOD first. HODs, the Principal and the Super Admin publish without approval.
- **A scheduler runs every minute.** It publishes scheduled notices when due and expires old ones.
- **Everything important is audited.** The Super Admin can read the full audit log.

### Roles

| Role | In short |
| --- | --- |
| Visitor | No account. Reads the public website and public notices, and can register. |
| Student | Reads notices meant for them, acknowledges, saves. Cannot create notices. |
| Teacher (Faculty) | Writes notices for students of their own department. The HOD must approve. May also be a class teacher. |
| HOD | Approves teachers' notices. Publishes for their own department. Approves department sign-ups. |
| Principal | Publishes to anyone without approval. Approves any sign-up, including HODs. |
| Super Admin | Sees everything. Manages users, departments, categories and the audit log. |

---

## UML Diagram Set: contents

The UML page contains these 17 diagrams:

| Group | Diagrams |
| --- | --- |
| Structure | Class Diagram · ER Diagram · Package Diagram |
| Architecture | Component Diagram · Deployment Diagram |
| Behaviour | Use Case Diagram · Activity Diagram |
| Sequences | Notice Approval · Registration & Login · Upload Attachment · AI Draft Notice |
| State machines | Notice Lifecycle · Account Status · Notification Status |
| Data flow | DFD Level 0 (Context) · DFD Level 1 · DFD Level 2 (Notices) |

Each diagram has **View Mermaid Code**, **Copy Code** and **Download SVG** buttons, so you can reuse them in a report or slides.

---

## Animated pages: contents

**Animated Project Flow**

1. The big picture: a clickable architecture diagram with moving request and response packets.
2. Registration and approval: the approver chain, and sign-in behaviour for each account status.
3. Life of a notice: a state machine you can drive as Teacher, HOD or Principal.
4. Who receives a notice: build an audience and watch matching people light up.
5. One request, step by step: the "Approve" click from the button to the database and back.
6. Time, visibility and the public site: drag a clock to see Scheduled, Published and Expired.

**Every Role Explained**

1. Role explorer: menu, dashboard, can and cannot do, and a day in the life for each role.
2. Permission matrix: 17 actions across 6 roles.
3. All roles story: one notice's journey through every role.
4. Try the locks: pick a person and an API call to see 401, 403 or 200.

---

## Project Handbook: contents

| § | Section | § | Section |
| --- | --- | --- | --- |
| 1 | Project Overview | 14 | Business Logic |
| 2 | Problem Statement | 15 | Security Features |
| 3 | Objectives | 16 | Error Handling |
| 4 | Complete Feature List | 17 | Validation |
| 5 | Technologies Used | 18 | Challenges Faced |
| 6 | Complete Architecture | 19 | Possible Improvements |
| 7 | Complete Folder Structure | 20 | Future Scope |
| 8 | Frontend | 21 | Expected Viva Questions (87) |
| 9 | Backend | 22 | Difficult Faculty Questions |
| 10 | Database | 23 | Complete Presentation Script |
| 11 | API Documentation (73 endpoints) | 24 | Complete Demo Script |
| 12 | Authentication | 25 | Quick Revision Notes |
| 13 | Application Workflow | | |

**For a viva or presentation:** use §21–22 for questions, §23 for the slide script, §24 for the live demo, and §25 for a 15-minute refresher.

---

## Numbers to remember

| Item | Value |
| --- | --- |
| Roles | 5 (plus visitors with no account) |
| Database tables | 12 |
| REST endpoints | 73 (12 are public) |
| Automated tests | 72 |
| Frontend routes | 29 |
| Scheduler interval | 1 minute |
| Login token (JWT) lifetime | 24 hours |
| Password-reset link | 30 minutes |
| Attachment download link | 5 minutes |
| Attachments | pdf, doc, docx, jpg, jpeg, png · 10 MB each · 10 per notice |

---

## Demo accounts

After starting the project, sign in with any of these. The password for all of them is `Password@123`.

| Email | Role |
| --- | --- |
| `admin@college.edu` | Super Admin |
| `principal@college.edu` | Principal |
| `hod.cs@college.edu` | HOD, Computer Engineering (Engineering) |
| `hod.dco@college.edu` | HOD, Computer Engineering (Polytechnic) |
| `faculty.cs@college.edu` | Teacher, Computer Engineering |
| `student.cs6a@college.edu` | Student, CS semester 6, class A |

---

## Running the project (short version)

Requirements: Java 17+, Node.js 18+, MySQL 8 (or Docker).

```bash
docker compose up -d                  # MySQL

cd backend && ./mvnw spring-boot:run  # API on http://localhost:8080
cd frontend && npm install && npm run dev   # app on http://localhost:5173
```

The first start creates all tables and loads demo data. Full setup and configuration are in the project's own `README.md` and in §5, §7 and §13 of the handbook.

---

## Known limits (also listed in the handbook)

Be ready to mention these honestly in a viva:

- Logout does not revoke the token (no refresh tokens yet).
- The login rate limiter is held in memory (Redis would be the fix).
- Editing a published notice does not notify recipients again.
- `ddl-auto=update` is for development, not production (use Flyway migrations).

---

## Credits

Built as a college project with Spring Boot, React and MySQL. Documentation, diagrams and animations are part of the project submission.
