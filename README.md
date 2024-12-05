# Database Management System

This project is a group university assignment aimed at developing a database management system with a REST API interface. The system is designed to handle various functional requirements related to course management, student enrollment, and academic operations.

## Project Overview

The purpose of this assignment is to:

1. Create SQL queries to support functional requirements
2. Develop a business logic layer with APIs for each functional requirement using NodeJS
3. Test and demonstrate results using Postman
4. Practice remote database connection and implement role-based access control

## Features

- SQL query creation for various database operations
- NodeJS and Express application for database connectivity
- RESTful APIs to support functional requirements
- Role-based access control for specific actions (e.g., course assignment, grading)
- Postman collection for API testing and demonstration

## Technologies Used

- SQL
- NodeJS
- Express
- MySQL2 package
- Postman

## Installation

Clone the project

```
git clone https://gitlab.csc.liv.ac.uk/sganiros/csck542_grp_project.git
```

Install the Packages.

```
npm install
```

## API

**All API calls should contain API Token or the requests will be rejected from the system**

### Admins

Admins should be able to enable or disable the availability of a course

```
POST 127.0.0.1:3000/api/v1/admin/course/availability
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `userID` | `int` | **Administrator ID** |
| `isAvailable` | `int` | **1(Available), 0(Unavailable)** |
| `courseID` | `int` | **Course ID** |

Admins should be able to assign one or more courses to a teacher

```
POST 127.0.0.1:3000/api/v1/admin/course/assign
```

 Parameter | Type | Description |
| :--- | :--- | :--- |
| `userID` | `int` | **Administrator ID** |
| `teacherID` | `int` | **Teacher ID** |
| `courses[]` | `int` | **Course ID** |

*Any amount of courses[] can be provided with this request since one teacher can be assigned to more than one course*

### Teachers

Teachers can fail or pass a student

```
POST 127.0.0.1:3000/api/v1/teacher/student/result
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `teacherID` | `int` | **Teacher ID** |
| `studentID` | `int` | **Student ID** |
| `courseID` | `int` | **Course ID** |
| `result` | `int` | **1(Pass), 0(Fail)** |

### Students

Students can browse and list all the available courses and see the course title and course teacher’s name.

```
GET 127.0.0.1:3000/api/v1/students/courses
```

Students can enrol in a course. Students should not be able to enrol in a course more than once at each time. 

```
POST 127.0.0.1:3000/api/v1/students/enrol
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `studentID` | `int` | **Student ID** |
| `courseID` | `int` | **Course ID** |

## Role-Based Access Control

The system implements role-based access control to restrict certain actions to specific roles. For example:
- Assigning courses to teachers is limited to college staff
- Pass/fail decisions are made by teachers

## Testing

Use Postman to test and demonstrate the results of executing the APIs. For guidance on sending your first request, refer to the [Postman Learning Center](https://learning.postman.com/docs/getting-started/sending-the-first-request/).
