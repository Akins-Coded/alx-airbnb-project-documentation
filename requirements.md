# 📋 Backend Feature Requirement Specifications – Airbnb Clone

This document outlines the detailed technical specifications for three core backend features:

* User Authentication
* Property Management
* Booking System

---

## 🔐 1. User Authentication

### Endpoints

| Method  | Endpoint            | Description            |
| ------- | ------------------- | ---------------------- |
| POST    | /api/auth/register/ | Register a new user    |
| POST    | /api/auth/login/    | Login and receive JWT  |
| POST    | /api/auth/refresh/  | Refresh access token   |
| GET/PUT | /api/users/me/      | View or update profile |

### Input/Output Specification

#### ✅ Registration

**Input (JSON):**

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "StrongPass123",
  "phone_number": "+2348012345678",
  "role": "guest"
}
```

**Output (Success):** `201 Created`

```json
{
  "id": "uuid",
  "email": "john@example.com",
  "role": "guest",
  "token": "JWT_TOKEN"
}
```

#### ✅ Login

**Input:**

```json
{
  "email": "john@example.com",
  "password": "StrongPass123"
}
```

**Output:** `200 OK`

```json
{
  "access": "JWT_ACCESS_TOKEN",
  "refresh": "JWT_REFRESH_TOKEN"
}
```

### Validation Rules

* Email must be unique and valid
* Password must be at least 8 characters
* Role must be one of: `guest`, `host`, `admin`

### Performance Criteria

* Response time: < 200ms
* Token generation must be stateless and secure
* Rate limit login attempts to prevent brute force

---

## 🏠 2. Property Management

### Endpoints

| Method | Endpoint              | Description             |
| ------ | --------------------- | ----------------------- |
| POST   | /api/properties/      | Add new property (host) |
| PUT    | /api/properties/<id>/ | Update property         |
| DELETE | /api/properties/<id>/ | Delete property         |
| GET    | /api/properties/      | List/search properties  |
| GET    | /api/properties/<id>/ | View property details   |

### Input/Output Specification

#### ✅ Create Property

**Input:**

```json
{
  "name": "Modern Apartment",
  "description": "Clean and spacious flat",
  "location": "Lagos, Nigeria",
  "pricepernight": 30000.00
}
```

**Output:** `201 Created`

```json
{
  "id": "uuid",
  "name": "Modern Apartment",
  "location": "Lagos, Nigeria",
  "host_id": "uuid"
}
```

### Validation Rules

* Name, description, location: required
* Price must be > 0
* Only users with `host` role can create or modify

### Performance Criteria

* List view supports pagination and filtering
* Caching may be applied to popular listings
* Ensure non-blocking DB queries for updates

---

## 📅 3. Booking System

### Endpoints

| Method | Endpoint                   | Description              |
| ------ | -------------------------- | ------------------------ |
| POST   | /api/bookings/             | Create a booking (guest) |
| GET    | /api/bookings/me/          | Guest booking history    |
| POST   | /api/bookings/<id>/cancel/ | Cancel booking           |

### Input/Output Specification

#### ✅ Create Booking

**Input:**

```json
{
  "property_id": "uuid",
  "start_time": "2025-07-01T12:00:00Z",
  "end_time": "2025-07-05T12:00:00Z"
}
```

**Output:** `201 Created`

```json
{
  "id": "uuid",
  "status": "pending",
  "total_price": 120000.00
}

### Validation Rules

* Date range must not overlap with existing bookings
* End time must be after start time
* Must be authenticated as a guest

### Performance Criteria

* Availability check must be optimized with DB indices
* Prevent race conditions using transaction locks
* Response time: < 300ms under load

```
#### ⭐ 4. Review System

## 🔸 Feature Summary

Allows guests to leave reviews for properties after a completed booking. Hosts may respond. Admins may moderate.

### 🔸 Endpoints

POST /api/reviews/

GET /api/properties/{id}/reviews/

DELETE /api/reviews/{id}/ (Admin only)

POST /api/reviews/{id}/reply/ (Host reply)

**🔸 Input**

/reviews/

```json

{
  "property_id": "uuid",
  "rating": 4,
  "comment": "Great stay, highly recommend!"
}


**🔸 Output**

```json
{
  "message": "Review submitted",
  "review_id": "uuid"
}

### Validation Rules

* Rating must be between 1 and 5
* Comment must not be empty
* Only one review per booking
* Only guests with completed bookings can review

### Performance Criteria

* Reviews should be retrievable per property in < 200ms
* Caching may be used for top-rated listings

---

**Note:** Note: All UUIDs refer to CHAR(36) primary keys.

These specifications ensure that each core feature is functional, secure, and performant in real-world conditions.