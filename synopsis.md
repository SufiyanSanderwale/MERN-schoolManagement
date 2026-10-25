# School Management System

## Project Synopsis

### 1. Project Title

**School Management System (SMS)**

### 2. Abstract

The School Management System is a web application built with the MERN stack: MongoDB, Express.js, React.js, and Node.js. It provides a shared platform for administrators, teachers, and students to manage and access school-related information.

The current application focuses on school setup and core academic workflows. An administrator can create classes, subjects, student accounts, and teacher accounts, publish notices, and review complaints. Teachers can view students in their assigned class, record attendance, and enter examination marks. Students can view their subjects, attendance, and marks, and submit complaints to the school.

The system uses a React frontend with Material UI and Redux for the user interface and client-side state. An Express API handles application requests, while Mongoose connects the backend to MongoDB. This synopsis describes the functionality evidenced in the current codebase and distinguishes it from recommendations for future development.

### 3. Introduction

Schools manage information about students, teachers, classes, subjects, attendance, assessments, and communications. When these activities are handled through separate records or manual processes, staff may spend extra time maintaining data, and students may not have a convenient way to review their academic information.

This project brings several of these workflows into one browser-based application. It provides role-specific dashboards so that administrators, teachers, and students can access the parts of the system relevant to them. The application is intended as a foundational school-management system and can be extended with additional operational features.

### 4. Problem Statement

Managing school information across disconnected or manual processes can make it difficult to:

- Maintain consistent records of classes, students, teachers, and subjects.
- Record and review student attendance.
- Enter and retrieve subject-level examination marks.
- Communicate school notices to users.
- Collect and review student complaints.
- Provide users with a role-appropriate view of school information.

The project addresses these needs by centralizing selected records and workflows in a web application. It does not yet cover every administrative process a school may require.

### 5. Project Objectives

The objectives of the current system are to:

1. Provide separate application experiences for administrators, teachers, and students.
2. Allow an administrator to create and manage core school records.
3. Associate students, teachers, and subjects with classes and a school.
4. Support recording student attendance by subject and date.
5. Support entering and viewing student examination marks.
6. Provide a school notice board.
7. Allow students to submit complaints and administrators to review them.
8. Present academic information through dashboards, tables, and charts where implemented.

### 6. Project Scope

#### 6.1 Included in the Current Implementation

- Admin registration and login.
- Teacher and student login.
- Class creation, listing, viewing, and deletion.
- Student creation, listing, viewing, updating, and deletion.
- Teacher creation, listing, viewing, deletion, and subject assignment.
- Subject creation, listing, viewing, and deletion.
- Student attendance recording and viewing, including selected attendance-clearing operations.
- Examination mark entry and viewing.
- Notice creation, listing, editing through a backend endpoint, and deletion.
- Student complaint submission and administrator complaint listing.
- Role-specific student, teacher, and administrator dashboard pages.
- Local MongoDB or MongoDB Atlas configuration through environment variables.

#### 6.2 Outside the Current Scope

The following are not complete features in the current codebase and are recommendations, not claims about existing functionality:

- Parent or guardian accounts.
- Fee collection, payment processing, and receipts.
- Timetable creation and scheduling.
- Homework distribution and submission.
- A complete complaint response and resolution workflow.
- Email, SMS, or push notifications.
- Attendance and results report export.
- Multi-term report cards and configurable grading policies.
- A production-grade authentication and authorization system.

### 7. User Roles and Responsibilities

#### Administrator

- Registers and signs in to the system.
- Creates classes, subjects, student accounts, and teacher accounts.
- Assigns teachers to subjects and classes through the available workflows.
- Views school records and student academic information.
- Publishes and manages notices.
- Reviews complaints submitted by students.
- Views administrator profile information.

#### Teacher

- Signs in to the system.
- Views the assigned class and its students.
- Records student attendance for the assigned subject.
- Enters or updates student examination marks.
- Views teacher profile information.

#### Student

- Signs in using the student credentials supported by the application.
- Views subjects, attendance, and examination marks.
- Submits a complaint to the school.
- Views student profile information.

### 8. Functional Requirements

The current implementation supports the following functional requirements:

| ID | Requirement |
|---|---|
| FR-01 | The system shall allow an administrator to register and sign in. |
| FR-02 | The system shall allow teachers and students to sign in. |
| FR-03 | The administrator shall be able to create and view classes. |
| FR-04 | The administrator shall be able to create, view, and delete subjects. |
| FR-05 | The administrator shall be able to add, view, update, and delete student records. |
| FR-06 | The administrator shall be able to add, view, and delete teacher records, and assign a teacher to a subject. |
| FR-07 | The system shall allow attendance to be recorded for a student, subject, date, and status. |
| FR-08 | The system shall allow examination marks to be recorded for a student and subject. |
| FR-09 | The administrator shall be able to create and view school notices. |
| FR-10 | Students shall be able to submit complaints, and administrators shall be able to view submitted complaints. |
| FR-11 | Students shall be able to view their subjects, attendance, and marks. |
| FR-12 | Teachers shall be able to view their assigned class and its student list. |

### 9. Non-Functional Requirements

These are quality goals for the system; some require further implementation and verification:

- **Usability:** The interface should be understandable to users with basic web-browser experience.
- **Performance:** Common school lists and details should load within a reasonable time for the expected dataset size.
- **Reliability:** Database and API errors should be reported clearly, and operations should not silently appear successful when they fail.
- **Data integrity:** Related records should remain consistent when classes, subjects, students, or teachers are changed or removed.
- **Security:** Passwords should be securely hashed, access should be authorized on the backend, and secrets should remain in environment variables.
- **Maintainability:** Frontend, API, controller, and database-model responsibilities should remain separated.
- **Compatibility:** The React application should work in modern browsers, and the backend should run on a supported Node.js runtime.

### 10. Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React 18, React Router, Redux Toolkit, Redux |
| UI | Material UI, Emotion, styled-components |
| Data visualization | Recharts |
| HTTP communication | Axios |
| Backend runtime | Node.js |
| API framework | Express.js |
| Database | MongoDB |
| Database object modeling | Mongoose |
| Password hashing | bcrypt for student and teacher accounts |
| Configuration | dotenv |
| Development server restart | nodemon |

### 11. System Architecture

The application follows a client-server architecture:

1. **React frontend:** Renders pages for each user role and dispatches API requests.
2. **Redux state layer:** Stores frontend state for users and selected domain data.
3. **Express REST API:** Receives HTTP requests and maps routes to controller functions.
4. **Controllers:** Apply application logic and read or write MongoDB records using Mongoose.
5. **MongoDB database:** Persists administrator, class, student, teacher, subject, notice, and complaint documents.

Typical request flow:

```text
User action
    -> React page/component
    -> Redux action or Axios request
    -> Express route
    -> Controller
    -> Mongoose model
    -> MongoDB
    -> API response
    -> Redux state and updated UI
```

### 12. Main Application Modules

#### 12.1 User and Dashboard Module

The application presents role-specific routes and dashboards for administrators, teachers, and students. User state is maintained on the frontend through Redux.

#### 12.2 Class Management Module

Administrators can create classes, list them, open class details, and remove classes. The backend also removes related class records in certain deletion workflows. Class editing and archival are not currently available.

#### 12.3 Student Management Module

Administrators can add students to classes, view student lists and details, update student records, and delete students. Student records include a class reference, school reference, exam results, and attendance entries.

#### 12.4 Teacher Management Module

Administrators can create teachers, view teacher lists and details, assign a class and subject through the available workflow, and delete teacher records. A complete teacher profile-editing workflow is not present.

#### 12.5 Subject Management Module

Administrators can create subjects with a subject name, code, session count, class, and school association. Subjects can be listed and viewed, and a teacher can be assigned. Full subject editing is not implemented in the current interface.

#### 12.6 Attendance Module

Teachers can record a student's attendance for a subject and date with a present or absent status. Existing attendance for the same student, subject, and date can be updated. Students can view their attendance. Administrative clearing operations are also exposed by the API.

#### 12.7 Examination Marks Module

Marks are stored as subject-level results on student records. Teachers can enter or update marks for students in their assigned class, while students can view their results.

#### 12.8 Notice Module

Administrators can create and list school notices. The backend includes an update endpoint and delete operations. The current listing interface provides deletion and navigation to add notices; a complete edit workflow should be verified and completed.

#### 12.9 Complaint Module

Students can submit a dated complaint. Administrators can view complaints with the submitting user's name. A response, status, assignment, and resolution lifecycle is not currently implemented. The teacher complaint page is only a placeholder.

### 13. Data Model Overview

The application defines the following main MongoDB models:

- **Admin:** name, email, password, role, and school name.
- **Class (Sclass):** class name and associated school.
- **Student:** name, roll number, password, class, school, exam results, and attendance.
- **Teacher:** name, email, password, role, school, assigned subject, assigned class, and attendance-related fields.
- **Subject:** subject name, subject code, session count, class, school, and optional teacher.
- **Notice:** title, details, date, and school.
- **Complaint:** submitting user, date, complaint text, and school.

Records are connected through MongoDB ObjectId references. Student attendance and marks are embedded arrays on the student document.

### 14. API Overview

The Express router exposes API groups for:

- Admin registration, login, and profile retrieval.
- Student registration, login, list/detail retrieval, updates, deletion, attendance, and marks.
- Teacher registration, login, list/detail retrieval, deletion, assignment, and attendance.
- Class creation, list/detail retrieval, student retrieval, and deletion.
- Subject creation, list/detail retrieval, class/school lists, free-subject lists, and deletion.
- Notice creation, list retrieval, update, and deletion.
- Complaint creation and list retrieval.

The routes are defined in `backend/routes/route.js`. This synopsis summarizes their purpose and is not a complete API specification.

### 15. Setup and Execution Summary

#### Prerequisites

- Node.js and npm.
- MongoDB Community Server running locally, or a reachable MongoDB Atlas database.

#### Backend

1. Install backend dependencies from the `backend` directory using `npm install`.
2. Create `backend/.env` with `MONGO_URL` and `SECRET_KEY`.
3. Start the API with `npm start`.

For a local MongoDB instance, the connection URL can be:

```env
MONGO_URL=mongodb://127.0.0.1:27017/smsproject
SECRET_KEY=replace-with-a-private-random-value
```

#### Frontend

1. Install frontend dependencies from the `frontend` directory using `npm install`.
2. Set `REACT_APP_BASE_URL=http://localhost:5000` in `frontend/.env`.
3. Start the React development server with `npm start`.

The development frontend normally runs at `http://localhost:3000`, and the backend at `http://localhost:5000`. Do not commit `.env` files or share their secret values.

### 16. Current Limitations and Recommended Improvements

The following points are important when evolving the current learning/demo application into a more complete system:

1. **Authentication and authorization:** Add secure session or token-based authentication and backend authorization checks for every protected operation. Frontend role-based navigation alone is not an access-control boundary.
2. **Administrator password handling:** The current admin controller does not use the bcrypt workflow used for student and teacher passwords. Apply password hashing consistently and migrate any existing administrator records safely.
3. **Validation and error handling:** Validate request data, return suitable HTTP status codes, and present actionable errors in the UI.
4. **CRUD completeness:** Add class editing, subject editing, teacher editing, and administrator profile/password management.
5. **Complaint workflow:** Add status, staff response, timestamps, and a way for the student to view progress.
6. **Deletion safety:** Provide confirmation, related-record impact information, and preferably archive/restore for destructive actions.
7. **Data consistency:** Review linked-record cleanup and make deletion/update operations consistent, including cases where related documents are missing.
8. **Input and uniqueness rules:** Enforce appropriate school-scoped uniqueness and validation for student roll numbers, teacher emails, subject codes, and other identifying fields.
9. **Audit history:** Track who changed attendance, marks, or key school records and when.
10. **Testing:** Add automated tests for controllers, routes, validation, and role-specific user flows.
11. **Operational readiness:** Add structured logging, database connection readiness checks, backups, and production configuration guidance.

### 17. Future Enhancements

Potential future modules include:

- Timetable and academic calendar management.
- Homework and assignment creation, submission, and grading.
- Parent or guardian accounts and student progress access.
- Fee management, invoices, payment status, and receipts.
- Notifications for notices, attendance, results, and complaint responses.
- Search, filtering, pagination, and bulk CSV import/export.
- Printable report cards and attendance summaries.
- Configurable terms, grading scales, and academic years.
- Accessibility and expanded mobile-device usability.

### 18. Expected Benefits

When used with appropriate security, validation, and operational controls, the system can:

- Centralize core academic records.
- Reduce repetitive manual entry across supported workflows.
- Give teachers a shared process for recording attendance and marks.
- Give students convenient access to selected academic information.
- Provide administrators with a central place to manage key school records and notices.
- Establish a foundation that can be extended with additional school services.

### 19. Conclusion

The School Management System is a MERN-based application that brings together foundational school-management workflows for administrators, teachers, and students. Its current implementation covers core records, attendance, marks, notices, and complaint submission. It is a useful base for learning and further development, but it should not be treated as production-ready until authentication, authorization, data validation, deletion safety, testing, and the incomplete management workflows have been addressed.
