Here's a complete `requirements.md` document covering three key backend features: **User Authentication**, **Property Management**, and **Booking System**. This includes API endpoints, input/output specs, validation rules, and performance criteria, as requested.

---

## 📄 requirements.md

````markdown
# Airbnb Clone – Backend Feature Requirements

## 1. User Authentication

### Description
Manages user registration, login, and profile access for Guests, Hosts, and Admins.

### API Endpoints

#### POST /api/auth/register
Registers a new user.

**Input:**
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "Secret123!",
  "role": "guest" // or "host"
}
````

**Validation:**

* Email must be unique and valid format.
* Password must be at least 8 characters, contain letters and numbers.
* Role must be either `guest` or `host`.

**Output:**

* 201 Created with confirmation message.
* Sends verification email.

#### POST /api/auth/login

Authenticates a user.

**Input:**

```json
{
  "email": "john@example.com",
  "password": "Secret123!"
}
```

**Output:**

* 200 OK with JWT access token.
* 401 Unauthorized if credentials are invalid.

#### GET /api/auth/profile

Fetches current user profile.

**Headers:**

* Authorization: Bearer `<token>`

**Output:**

```json
{
  "id": "user_id",
  "firstName": "John",
  "email": "john@example.com",
  "role": "host"
}
```

### Performance Criteria

* Response time < 500ms.
* Token expiry: 24 hours.
* Secure password hashing using bcrypt.

---

## 2. Property Management

### Description

Allows Hosts to create, update, and manage property listings.

### API Endpoints

#### POST /api/properties

Creates a new property listing.

**Input:**

```json
{
  "title": "Cozy Apartment in Downtown",
  "description": "2-bedroom apartment close to all amenities.",
  "location": "New York, NY",
  "amenities": ["WiFi", "Kitchen", "Washer"],
  "pricePerNight": 150,
  "photos": ["url1.jpg", "url2.jpg"],
  "availability": {
    "startDate": "2025-06-01",
    "endDate": "2025-12-31"
  }
}
```

**Validation:**

* Title must be present.
* Price must be a positive number.
* At least one photo required.
* Availability dates must be valid.

**Output:**

* 201 Created with listing ID.

#### PUT /api/properties/\:id

Updates an existing listing.

**Headers:**

* Authorization: Bearer `<token>`

**Input:** Same structure as POST with fields to update.

**Output:**

* 200 OK with updated property data.

#### GET /api/properties?location=NYC\&priceMin=100\&priceMax=300

Searches for properties.

**Output:**
List of matching property summaries.

### Performance Criteria

* Full-text search optimized on `location` and `title`.
* Image upload via external service (e.g., AWS S3).

---

## 3. Booking System

### Description

Manages guest bookings for properties including availability check, payment linkage, and confirmation.

### API Endpoints

#### POST /api/bookings

Creates a booking request.

**Input:**

```json
{
  "propertyId": "123",
  "checkIn": "2025-07-01",
  "checkOut": "2025-07-07",
  "guests": 2
}
```

**Validation:**

* Dates must be valid and not overlap with existing bookings.
* Guests must not exceed property limit.

**Output:**

* 201 Created with booking details and total price.
* Redirects to `/api/payments/initiate`.

#### GET /api/bookings/\:id

Fetches a single booking.

**Output:**

```json
{
  "bookingId": "abc123",
  "propertyId": "123",
  "guestId": "xyz789",
  "status": "pending" // or "confirmed", "cancelled"
}
```

#### DELETE /api/bookings/\:id

Cancels a booking.

**Output:**

* 200 OK with refund status if eligible.

### Performance Criteria

* Booking conflict checks must complete in <200ms.
* Atomic transaction across booking and payment initiation.

---

## Security & Compliance

* All endpoints use HTTPS and JWT authentication.
* Rate limiting on sensitive endpoints (e.g., login, register).
* GDPR-compliant user data handling.

---

## To Do

* Add payment gateway integration in `/api/payments`.
* Add email notifications on booking status changes.
