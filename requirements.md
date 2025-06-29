# 📋 Airbnb Clone Backend Requirements

This document specifies the **technical** and **functional** requirements for key backend features of the Airbnb Clone project. It includes API endpoints, request/response formats, validations, and performance considerations.

 User Authentication

Functional Requirements
 Users can register as guests or hosts.
 Users can log in securely using JWT.
 Only authenticated users can access protected routes.

API Endpoints
POST `/api/auth/register`
 <!-- **Description**: Register a new user. -->
  <!-- **Input**: -->
  ```json
  {
    "first_name": "Jane",
    "last_name": "Doe",
    "email": "jane@example.com",
    "password": "MySecurePass123",
    "role": "host"
  }

This document outlines the technical and functional requirements for key backend features in the Airbnb Clone project.

---

## 1. User Authentication

### Description
Handles user registration, login, and authentication using JWT.

### API Endpoints
- `POST /api/register`
- `POST /api/login`
- `GET /api/profile` (protected)

### Input
#### Register:
```json
{
  "first_name": "Alice",
  "last_name": "Walker",
  "email": "alice@example.com",
  "password": "SecurePassword123"
}
```

Login:
```json
{
  "email": "alice@example.com",
  "password": "SecurePassword123"
}
```

Output
 JWT token on success
Error messages on validation failure or invalid credentials

Validation Rules
 Email must be valid and unique
 Password must be at least 8 characters
All fields are required

Performance Criteria
  Response time under 200ms
 JWT token valid for 24 hours

---

2. Property Management

Description
Allows hosts to manage property listings.

 API Endpoints
 `POST /api/properties`
  `PUT /api/properties/:id`
 `DELETE /api/properties/:id`
 `GET /api/properties`

Input
 Create Listing:
```json
{
  "title": "Beach House",
  "description": "A cozy home near the beach",
  "location": "Cape Coast",
  "pricepernight": 250.00,
  "amenities": ["Wi-Fi", "Pool"]
}
```

 Output
 Confirmation message with new property ID
 List of properties with filters applied (on `GET`)

 Validation Rules
  Title, description, location, and price must not be empty
 Price must be positive

Performance Criteria
 Listings fetched under 300ms with pagination
 Listings cached if frequently accessed

---

 3. Booking System

 Description
Manages bookings from guests for listed properties.
 API Endpoints
 `POST /api/bookings`
 `DELETE /api/bookings/:id`
 `GET /api/bookings/:userId`

Input
Create Booking:
```json
{
  "property_id": "aaaa-1111",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05"
}
```

ooking ID and confirmation message
  Booking status updates
 Validation Rules
 Dates must not overlap with existing bookings
 start_date < end_date
 Property must exist

 Performance Criteria
 Prevents double booking within 50ms of submission
 Booking confirmation returned under 300ms