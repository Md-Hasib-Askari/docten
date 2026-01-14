# Docten - Medical Practice Management System

## Overview

Docten is a comprehensive full-stack medical practice management system designed to streamline healthcare operations. The application enables doctors to manage patients, appointments, staff, and prescriptions efficiently through a modern web interface. Built with scalability and user experience in mind, it provides a complete solution for medical practices to digitize their workflow.

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

## Features

### Core Functionalities

#### Patient Management
- Add, edit, and view patient records
- Track patient demographics (name, age, weight, phone, address)
- Search and filter patient database
- Instant patient registration during appointments

#### Appointment Management
- Schedule appointments with date and time
- Track appointment status (upcoming, completed, cancelled)
- View appointment history and notes
- Link appointments to prescriptions
- Dashboard metrics for appointment analytics

#### Prescription Management
- Digital prescription generation
- Medication management with dosage and frequency
- Patient complaints and medical history tracking
- Diagnosis and investigation records
- Follow-up date scheduling
- Print-ready prescription templates
- Prescription snapshots for record-keeping

#### Staff Management
- Staff registration and profile management
- Role-based access control (Doctor, Staff, Patient)
- Staff status tracking (active, inactive, vacation)
- Staff directory with contact information

#### Doctor Profile
- Professional profile with credentials
- Multiple degree support
- Specialization and designation
- BMDC (Bangladesh Medical & Dental Council) number
- Digital signature integration
- Multiple contact numbers

#### Authentication & Authorization
- Secure user registration and login
- JWT-based authentication
- Role-based access control (RBAC)
- Password reset with OTP verification
- Email verification
- Account activation system
- Secure cookie-based session management

#### Dashboard Analytics
- Real-time metrics for:
  - Total patients
  - Total appointments
  - Upcoming appointments
  - Staff count
- Tabbed interface for different management areas
- Visual analytics with cards and charts

## Technology Stack

### Frontend

- **Framework**: Next.js 14.2.14 (React 18)
- **Language**: TypeScript 5
- **UI Library**: NextUI 2.4.8
- **Styling**: Tailwind CSS 3.4.1
- **State Management**: Zustand 5.0.0
- **Form Management**: Formik 2.4.6 with Yup validation
- **HTTP Client**: Axios 1.7.7
- **Icons**: Lucide React, React Icons
- **Additional Libraries**:
  - react-to-print for prescription printing
  - moment.js for date handling
  - libphonenumber-js for phone validation
  - react-hot-toast for notifications

### Backend

- **Runtime**: Node.js 20.18.1
- **Framework**: Express.js 4.21.0
- **Language**: TypeScript 5.6.2
- **Database**: MongoDB with Mongoose 8.7.0
- **Authentication**: JWT (jsonwebtoken 9.0.2)
- **Password Hashing**: bcryptjs 2.4.3
- **Email Service**: Nodemailer 6.9.15
- **File Upload**: Multer 1.4.5
- **Validation**: Express-validator 7.2.0
- **Security Middleware**:
  - Helmet 8.0.0 (HTTP headers security)
  - CORS 2.8.5
  - HPP 0.2.3 (HTTP Parameter Pollution protection)
  - express-rate-limit 7.4.1

### DevOps

- **Containerization**: Docker with Docker Compose
- **Development Tools**:
  - ts-node-dev for hot reloading
  - ESLint for code linting
  - Prettier for code formatting

## Architecture

The application follows a monorepo structure with clear separation between client and server:

```
docten/
├── client/          # Next.js frontend application
├── server/          # Express.js backend API
└── docker-compose.yaml  # Container orchestration
```

### Frontend Architecture

- **App Router**: Utilizes Next.js 14 App Router for routing
- **Component-Based**: Modular component structure with reusable UI elements
- **API Layer**: Centralized API service layer for backend communication
- **State Management**: Zustand stores for auth, dashboard, prescription, and profile state
- **Type Safety**: Comprehensive TypeScript interfaces and types

### Backend Architecture

- **MVC Pattern**: Separation of concerns with Models, Controllers, and Routes
- **Middleware Pipeline**: Authentication, validation, and error handling
- **RESTful API**: Consistent API design following REST principles
- **Database Layer**: Mongoose ODM for MongoDB interactions
- **Service Layer**: Helper functions for auth, token management, and user roles

## Prerequisites

Before running the application, ensure you have the following installed:

- **Node.js**: Version 20.x or higher
- **npm**: Version 9.x or higher
- **MongoDB**: Version 6.x or higher (local or cloud instance)
- **Docker** (optional): For containerized deployment
- **Docker Compose** (optional): For multi-container orchestration

## Installation

### Local Development Setup

#### 1. Clone the Repository

```bash
git clone https://github.com/Md-Hasib-Askari/docten.git
cd docten
```

#### 2. Install Client Dependencies

```bash
cd client
npm install
```

#### 3. Install Server Dependencies

```bash
cd ../server
npm install
```

### Docker Setup

If using Docker, no manual installation is needed. Docker will handle all dependencies.

## Configuration

### Client Configuration

Create a `.env` file in the `client` directory:

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api/v1
NEXT_PUBLIC_API_STATIC_URL=http://localhost:5000/uploads
```

### Server Configuration

Create a `.env` file in the `server` directory based on `.env.example`:

```env
# Database
MONGODB_CONNECTION=mongodb://localhost:27017/docten

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here
REFRESH_TOKEN_SECRET=your_refresh_token_secret_here
TOKEN_NAME=token

# Password Hashing
SALT_ROUNDS=10

# Email Configuration (for OTP and notifications)
EMAIL_USER=your_email@example.com
EMAIL_PASS=your_email_password

# Client URL (for CORS and email links)
CLIENT_URL=http://localhost:3000

# Server Port
PORT=5000
```

## Running the Application

### Local Development

#### Start MongoDB

Make sure MongoDB is running on your local machine:

```bash
mongod
```

#### Run Backend Server

```bash
cd server
npm run dev
```

The server will start on `http://localhost:5000`

#### Run Frontend Application

```bash
cd client
npm run dev
```

The client will start on `http://localhost:3000`

### Docker Deployment

Build and run both services using Docker Compose:

```bash
docker-compose up --build
```

This will:
- Build the Next.js frontend container
- Build the Express backend container
- Create a bridge network for inter-container communication
- Start both services
- Frontend: `http://localhost:3000`
- Backend: `http://localhost:5000`

To run in detached mode:

```bash
docker-compose up -d
```

To stop the containers:

```bash
docker-compose down
```

## Project Structure

### Client Structure

```
client/
├── public/                    # Static assets
│   └── prescription.json      # Prescription templates
├── src/
│   ├── api/                   # API service layer
│   │   ├── api.ts            # Base API configuration
│   │   └── dashboard/        # Dashboard API endpoints
│   ├── app/                   # Next.js app directory
│   │   ├── page.tsx          # Landing page
│   │   ├── auth/             # Authentication pages
│   │   │   ├── page.tsx      # Login page
│   │   │   ├── enter-otp.tsx
│   │   │   ├── forget-password.tsx
│   │   │   └── reset-password.tsx
│   │   ├── dashboard/        # Dashboard pages
│   │   │   ├── page.tsx      # Main dashboard
│   │   │   ├── appointments/ # Appointment management
│   │   │   ├── patients/     # Patient management
│   │   │   ├── prescription/ # Prescription management
│   │   │   ├── staffs/       # Staff management
│   │   │   └── profile/      # Profile management
│   │   └── globals.css       # Global styles
│   ├── components/            # Reusable components
│   │   ├── auth/             # Auth-related components
│   │   ├── dashboard/        # Dashboard components
│   │   ├── globals/          # Global UI components
│   │   ├── landing-page/     # Landing page sections
│   │   └── prescription/     # Prescription components
│   ├── config/               # Configuration files
│   │   └── axios.ts          # Axios configuration
│   ├── data/                 # Static data
│   │   ├── degrees.ts        # Medical degrees list
│   │   └── specializations.json
│   ├── store/                # Zustand state stores
│   │   ├── auth-store.ts
│   │   ├── dashboard-store.ts
│   │   ├── prescription-store.ts
│   │   └── profile-store.ts
│   ├── types/                # TypeScript type definitions
│   │   ├── dashboard.ts
│   │   └── prescription.ts
│   └── utilities/            # Utility functions
│       └── timeZone.ts
├── Dockerfile                # Docker configuration
├── next.config.mjs           # Next.js configuration
├── tailwind.config.ts        # Tailwind CSS configuration
└── tsconfig.json             # TypeScript configuration
```

### Server Structure

```
server/
├── src/
│   ├── Controllers/          # Request handlers
│   │   ├── userController.ts
│   │   ├── auth/            # Authentication controllers
│   │   │   ├── authController.ts
│   │   │   ├── forgetPassword.ts
│   │   │   └── tokenController.ts
│   │   └── dashboard/       # Dashboard controllers
│   │       ├── appointment.ts
│   │       ├── doctor.ts
│   │       ├── medicine.ts
│   │       ├── patient.ts
│   │       ├── prescription.ts
│   │       └── staff.ts
│   ├── Helpers/             # Helper functions
│   │   ├── authVerify.ts
│   │   ├── tokenHelper.ts
│   │   └── userRole.ts
│   ├── Middlewares/         # Express middlewares
│   │   ├── authenticate.ts  # JWT authentication
│   │   ├── multerConfig.ts  # File upload configuration
│   │   └── validate.ts      # Request validation
│   ├── Models/              # Mongoose schemas
│   │   ├── userModel.ts
│   │   ├── subscription.ts
│   │   ├── dashboard/       # Dashboard models
│   │   │   ├── appointment.ts
│   │   │   ├── medicine.ts
│   │   │   └── prescription.ts
│   │   └── profile/         # Profile models
│   │       ├── doctor.ts
│   │       ├── patient.ts
│   │       └── staff.ts
│   ├── Routes/              # API route definitions
│   │   ├── authRoutes.ts
│   │   ├── userRoutes.ts
│   │   ├── appointmentRoutes.ts
│   │   └── prescription.ts
│   └── Validators/          # Input validation schemas
│       └── doctorValidator.ts
├── uploads/                 # File upload directory
│   └── prescriptions/       # Prescription snapshots
├── index.ts                 # Express app configuration
├── server.ts                # Server entry point
├── Dockerfile               # Docker configuration
└── tsconfig.json            # TypeScript configuration
```

## API Documentation

### Base URL

- **Local Development**: `http://localhost:5000/api/v1`
- **Docker**: `http://backend:5000/api/v1`

### Authentication Endpoints

#### POST `/register`
Register a new user account.

**Request Body:**
```json
{
  "email": "doctor@example.com",
  "password": "securePassword123",
  "role": "doctor"
}
```

#### POST `/login`
Authenticate user and receive JWT token.

**Request Body:**
```json
{
  "email": "doctor@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "success": true,
  "token": "jwt_token_here",
  "user": {
    "email": "doctor@example.com",
    "role": "doctor"
  }
}
```

#### GET `/authenticate`
Verify if the user is authenticated.

**Headers:** `Authorization: Bearer <token>`

#### GET `/logout`
Logout user and invalidate token.

#### POST `/activate`
Activate user account after registration.

#### POST `/forgot-password/send-otp`
Send OTP to email for password reset.

#### POST `/forgot-password/verify-otp`
Verify OTP for password reset.

#### POST `/forgot-password/reset-password`
Reset password using verified OTP.

### User Endpoints

#### GET `/profile`
Get authenticated user's profile information.

**Headers:** `Authorization: Bearer <token>`

#### GET `/dashboard/metrics`
Get dashboard analytics and metrics.

**Response:**
```json
{
  "success": true,
  "data": {
    "totalAppointmentCount": 150,
    "upcomingAppointmentCount": 25,
    "patientsCount": 300
  }
}
```

### Appointment Endpoints

All appointment endpoints require authentication.

#### POST `/appointments`
Create a new appointment.

#### GET `/appointments`
Get all appointments.

#### PUT `/appointments/:id`
Update appointment details.

#### DELETE `/appointments/:id`
Delete an appointment.

### Prescription Endpoints

All prescription endpoints require authentication.

#### POST `/prescriptions`
Create or update a prescription.

**Request Body:**
```json
{
  "appointmentId": "appointment_id",
  "medications": [],
  "instructions": [],
  "complaints": [],
  "history": [],
  "diagnosisList": [],
  "investigations": [],
  "followUpDate": "2026-02-01"
}
```

#### GET `/prescriptions/:appointmentId`
Get prescription by appointment ID.

### Patient Endpoints

#### POST `/patients`
Add a new patient.

#### GET `/patients`
Get all patients.

#### PUT `/patients/:id`
Update patient information.

#### DELETE `/patients/:id`
Delete a patient record.

### Staff Endpoints

#### POST `/staffs`
Add new staff member.

#### GET `/staffs`
Get all staff members.

#### PUT `/staffs/:id`
Update staff information.

#### DELETE `/staffs/:id`
Remove staff member.

## Database Schema

### Collections

#### Users
```javascript
{
  email: String (unique, required),
  password: String (hashed, required),
  role: String (enum: ['doctor', 'staff', 'patient']),
  userId: ObjectId (reference to Doctor/Staff/Patient),
  reset: {
    otp: String,
    attempt: Number,
    lastReset: Date
  },
  active: Boolean,
  isProfile: Boolean,
  timestamps: true
}
```

#### Doctors
```javascript
{
  name: String,
  degrees: [String],
  designation: String,
  specialization: String,
  phone: [String],
  bmdcNumber: String,
  digitalSignature: String,
  profileImage: String
}
```

#### Patients
```javascript
{
  name: String,
  age: Number,
  weight: Number,
  phone: String,
  address: String
}
```

#### Appointments
```javascript
{
  patientName: String,
  phone: String,
  date: String,
  time: String,
  note: String,
  snapshot: String,
  status: String (enum: ['upcoming', 'completed', 'cancelled']),
  doctorId: ObjectId
}
```

#### Prescriptions
```javascript
{
  appointmentId: ObjectId (unique),
  medications: [{
    medicationId: String,
    medication: String,
    duration: String,
    frequency: String,
    note: String
  }],
  instructions: [String],
  complaints: [String],
  history: [String],
  diagnosisList: [String],
  investigations: [String],
  followUpDate: Date,
  snapshot: String
}
```

#### Staff
```javascript
{
  name: String,
  role: String,
  phone: String,
  address: String,
  status: String (enum: ['active', 'inactive', 'vacation'])
}
```

## Security

### Implementation

1. **Authentication**: JWT-based token authentication with httpOnly cookies
2. **Password Security**: Bcrypt hashing with configurable salt rounds
3. **Rate Limiting**: 100 requests per 15 minutes per IP
4. **HTTP Headers**: Helmet middleware for secure HTTP headers
5. **CORS**: Configured for specific origins only
6. **Input Validation**: Express-validator for request validation
7. **Parameter Pollution**: HPP middleware to prevent HTTP parameter pollution
8. **XSS Protection**: Built-in sanitization and validation
9. **Role-Based Access Control**: Middleware for role verification
10. **OTP Verification**: Time-limited OTP for password reset with attempt limits

### Best Practices

- Never commit `.env` files to version control
- Use strong JWT secrets (at least 32 characters)
- Regularly update dependencies for security patches
- Use HTTPS in production
- Implement proper error handling without exposing sensitive information
- Regular security audits and penetration testing

## Contributing

### Development Workflow

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit changes: `git commit -m 'Add some feature'`
4. Push to branch: `git push origin feature/your-feature-name`
5. Submit a pull request

### Code Standards

- Follow TypeScript best practices
- Use ESLint and Prettier for code formatting
- Write meaningful commit messages
- Add comments for complex logic
- Update documentation for new features
- Write unit tests for critical functionality

### Coding Guidelines

- Use descriptive variable and function names
- Keep functions small and focused
- Follow the existing project structure
- Use TypeScript interfaces for type safety
- Handle errors gracefully
- Validate all user inputs

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

## Authors
- Md Hasib Askari - [GitHub](https://github.com/Md-Hasib-Askari)
- Moh. Asraful Hasan Asif - [GitHub](https://github.com/asif1416)

## Support

For support, create an issue in the repository.

## Roadmap

### Upcoming Features

- Mobile application (React Native)
- Patient portal for appointment booking
- SMS notifications for appointments
- Advanced analytics and reporting
- Multi-language support
- Telemedicine integration
- Laboratory test integration
- Billing and invoicing system
- Inventory management for medicines
- Backup and data export functionality

### Performance Improvements

- Implement caching strategies
- Optimize database queries
- Add pagination for large datasets
- Implement lazy loading
- Reduce bundle size

## Acknowledgments

- Next.js team for the amazing framework
- NextUI for beautiful UI components
- MongoDB team for the flexible database
- All open-source contributors whose libraries made this possible
