# 🏡 Airbnb Clone – Backend

This is a backend implementation of an Airbnb-like rental marketplace built with **Django Rest Framework (DRF)**. It supports **user authentication**, **property management**, **booking**, **payment processing**, **reviews**, **messaging**, and more.

---

## 🚀 Tech Stack

- **Django** + **Django Rest Framework**
- **Simple JWT** for token authentication
- **OAuth2** (Google) for social login
- **Paystack** / **Flutterwave** for payment integration
- **MYSQL** / **PostgreSQL** (or any other SQL-based DB)
- **Cloudinary/AWS S3** for image storage (optional)

---

## 🔑 Features

### 🔐 Authentication
- User registration & login (guest, host, admin roles)
- JWT token-based auth with refresh/blacklist
- Google OAuth2 login

### 🧑‍💼 User Management
- View/update profile
- Admin control over all users

### 🏠 Property Listings
- Create, update, delete listings (for hosts)
- Public search and filters
- Prevent deletion of booked properties

### 📅 Bookings
- Book property with date validation
- Manage booking status (pending, confirmed, cancelled)
- Guest and host booking history

### 💳 Payments
- Integration with **Paystack** or **Flutterwave**
- Payment confirmation via webhooks
- Transaction record storage

### ⭐ Reviews
- Guests leave reviews post-booking
- Hosts can respond to reviews
- Admin moderation support

### ✉️ Messaging
- Private messaging between users

### 🔔 Notifications
- Email updates (booking, payment, onboarding)

### 🛡 Security
- HTTPS-ready, rate limiting, SQL injection protection
- Password hashing, token rotation

---

## 🧪 Testing
- Unit and integration tests using `pytest`
- Covered: authentication, CRUD, booking, payments

---

## 📁 API Documentation
Available via Swagger/OpenAPI at `/docs/`

## 📁 Environment Variables
SECRET_KEY=
DEBUG=True
DATABASE_URL=
CLOUDINARY_URL=
PAYSTACK_SECRET_KEY=
FLUTTERWAVE_SECRET_KEY=
GOOGLE_CLIENT_ID=



---

## 📌 **API Endpoint List (Sample)**

| Feature              | Endpoint                                 | Method | Auth Required | Description                              |
|----------------------|-------------------------------------------|--------|----------------|------------------------------------------|
| Register             | `/api/auth/register/`                     | POST   | ❌              | Create a new user                        |
| Login                | `/api/auth/login/`                        | POST   | ❌              | Login and receive JWT                    |
| Refresh Token        | `/api/auth/refresh/`                      | POST   | ❌              | Refresh access token                     |
| Google OAuth         | `/api/auth/oauth/google/`                 | POST   | ❌              | Login/register with Google               |
| Profile View/Update  | `/api/users/me/`                          | GET/PUT| ✅              | View or update own profile               |
| Create Property      | `/api/properties/`                        | POST   | ✅ (host)       | Add a new property                       |
| Edit Property        | `/api/properties/<id>/`                   | PUT    | ✅ (host)       | Update own listing                       |
| Delete Property      | `/api/properties/<id>/`                   | DELETE | ✅ (host)       | Delete own listing                       |
| List Properties      | `/api/properties/`                        | GET    | ❌              | Search/filter property listings          |
| Create Booking       | `/api/bookings/`                          | POST   | ✅ (guest)      | Create a booking                         |
| Cancel Booking       | `/api/bookings/<id>/cancel/`              | POST   | ✅              | Cancel a booking                         |
| Booking History      | `/api/bookings/me/`                       | GET    | ✅              | Get user’s bookings                      |
| Payment Webhook      | `/api/payments/webhook/`                  | POST   | ❌              | Receive payment confirmation             |
| Submit Review        | `/api/reviews/`                           | POST   | ✅              | Leave review after completed booking     |
| Get Property Reviews | `/api/properties/<id>/reviews/`           | GET    | ❌              | View all reviews for a property          |
| Send Message         | `/api/messages/`                          | POST   | ✅              | Send message to another user             |
| Admin Panel          | `/admin/`                                 | GUI    | ✅ (admin)      | Django admin dashboard                   |

> This is a base version. Endpoint paths may vary depending on the `urls.py` file.

---

## 📝 Summary of Functional Requirements (Condensed)

This backend enables an Airbnb-style platform using Django Rest Framework, JWT, OAuth, and payment gateways. Key features include:

### 1. Authentication & Users
- Register/login with email or Google OAuth
- Token-based session via Simple JWT
- Role-based permissions (guest, host, admin)
- Profile viewing and editing

### 2. Property Management
- Hosts can create, edit, and delete listings
- Listings searchable by location, price, and filters
- Protect listings with active bookings

### 3. Bookings
- Guests can book properties with time/date validation
- Hosts and guests can cancel bookings
- View booking history

### 4. Payments
- Integration with Paystack/Flutterwave
- Webhook validation for successful transactions
- Supports credit card, bank transfer

### 5. Reviews
- Only guests with completed bookings can review
- Admins moderate content
- Hosts can reply to reviews

### 6. Messaging
- Users can send and receive private messages

### 7. Notifications
- Email alerts for bookings, cancellations, and payments

### 8. Admin Panel
- Manage users, bookings, reviews, listings, and payments

### 9. Media Storage
- Property and profile images via local/cloud storage

### 10. Security
- HTTPS, rate limiting, JWT rotation, input validation

### 11. Testing
- Unit/integration tests using pytest for all modules

