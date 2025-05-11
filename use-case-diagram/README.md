# Airbnb Clone - Use Case Descriptions

## Primary Actors

### 1. Guest
A user who searches for and books properties on the platform. Guests can view listings, make bookings, write reviews, and make payments.

### 2. Host
A user who lists and manages their properties on the platform. Hosts can create and update property listings, manage bookings, respond to reviews, and receive payments.

### 3. Admin
A system administrator who manages users, monitors listings, handles disputes, and generates reports.

### 4. Payment System (External)
An external payment processing system that handles payment transactions, including guest payments, host payouts, and refunds.

### 5. Email System (External)
An external email service that handles sending notifications to users.

## Use Cases

### Authentication

#### UC-1: Register Account
**Actor:** Guest, Host
**Description:** New users can create an account by providing personal information, email, and password.
**Flow:**
1. User selects "Sign Up" option
2. System displays registration form
3. User enters required information
4. System validates information
5. System creates user account
6. System sends verification email
7. User verifies email address
8. System activates user account

#### UC-2: Login to System
**Actor:** Guest, Host, Admin
**Description:** Registered users can log in to access their account and related functionalities.
**Flow:**
1. User enters email and password
2. System validates credentials
3. System grants access to user account
4. System displays appropriate dashboard based on user role

#### UC-3: Manage Profile
**Actor:** Guest, Host
**Description:** Users can view and update their profile information, including personal details, profile picture, and preferences.
**Flow:**
1. User selects "Profile" option
2. System displays current profile information
3. User makes changes to profile information
4. System validates and saves changes

### Property Management

#### UC-4: Create Property Listing
**Actor:** Host
**Description:** Hosts can create new property listings by providing details about their property.
**Flow:**
1. Host selects "Add New Listing" option
2. System displays property listing form
3. Host enters property details (name, description, location, amenities, etc.)
4. Host uploads property photos
5. Host sets availability and pricing
6. System validates information
7. System creates property listing

#### UC-5: Update Property Listing
**Actor:** Host
**Description:** Hosts can modify existing property listings.
**Flow:**
1. Host selects a property listing
2. System displays property details
3. Host updates desired information
4. System validates and saves changes

#### UC-6: Set Availability Calendar
**Actor:** Host
**Description:** Hosts can specify which dates their property is available for booking.
**Flow:**
1. Host selects calendar for a property
2. System displays calendar view
3. Host marks dates as available or unavailable
4. System saves availability settings

### Search and Booking

#### UC-7: Search Properties
**Actor:** Guest
**Description:** Guests can search for properties based on various criteria.
**Flow:**
1. Guest enters search criteria (location, dates, guests)
2. Guest applies filters (price range, amenities, etc.)
3. System displays matching properties
4. Guest can sort results by different criteria

#### UC-8: Book Property
**Actor:** Guest
**Description:** Guests can book a property for specific dates.
**Main Flow:**
1. Guest selects a property listing
2. Guest reviews property details
3. Guest selects check-in and check-out dates
4. Guest enters number of guests
5. System confirms availability
6. System calculates total price
7. Guest confirms booking
8. System redirects to payment
9. Guest completes payment
10. System confirms booking
11. System notifies host

**Alternative Flow - Property Unavailable:**
1. System informs guest that property is unavailable for selected dates
2. System suggests alternative dates

#### UC-9: Cancel Booking
**Actor:** Guest, Host
**Description:** Users can cancel an existing booking.
**Flow:**
1. User selects booking to cancel
2. System displays cancellation policy and potential refund
3. User confirms cancellation
4. System updates booking status
5. System initiates refund if applicable
6. System notifies other party

### Payment Processing

#### UC-10: Make Payment
**Actor:** Guest, Payment System
**Description:** Guests can make payments for their bookings.
**Flow:**
1. System calculates total amount
2. Guest selects payment method
3. System connects to payment gateway
4. Guest enters payment details
5. Payment system processes payment
6. System receives payment confirmation
7. System updates booking status

#### UC-11: Process Refund
**Actor:** Admin, Payment System
**Description:** The system processes refunds for canceled bookings.
**Flow:**
1. System determines refund amount based on cancellation policy
2. System initiates refund through payment gateway
3. Payment system processes refund
4. System receives refund confirmation
5. System updates payment status
6. System notifies guest

#### UC-12: Receive Payout
**Actor:** Host, Payment System
**Description:** Hosts receive payments for completed bookings.
**Flow:**
1. System identifies completed bookings eligible for payout
2. System calculates host payout amount (minus platform fees)
3. System initiates payout through payment gateway
4. Payment system processes payout
5. System updates payment status
6. System notifies host

### Reviews and Ratings

#### UC-13: Write Review
**Actor:** Guest
**Description:** Guests can write reviews and rate properties after their stay.
**Flow:**
1. System identifies completed bookings eligible for review
2. Guest selects "Write Review" option for a booking
3. Guest provides rating and written review
4. System validates review
5. System publishes review
6. System notifies host

#### UC-14: Respond to Review
**Actor:** Host
**Description:** Hosts can respond to reviews left by guests.
**Flow:**
1. Host views reviews for their property
2. Host selects "Respond" option for a specific review
3. Host writes response
4. System validates response
5. System publishes response
6. System notifies guest

### Notifications

#### UC-15: Receive Notifications
**Actor:** Guest, Host, Email System
**Description:** Users receive notifications about relevant activities.
**Flow:**
1. System generates notification based on trigger event (booking, message, payment, etc.)
2. System sends in-app notification
3. System sends email notification through email service
4. User receives and views notification

### Admin Functions

#### UC-16: Manage Users
**Actor:** Admin
**Description:** Administrators can view, edit, and manage user accounts.
**Flow:**
1. Admin accesses user management section
2. System displays list of users
3. Admin can search/filter users
4. Admin can view user details
5. Admin can suspend/activate user accounts

#### UC-17: Handle Disputes
**Actor:** Admin
**Description:** Administrators can mediate disputes between guests and hosts.
**Flow:**
1. Admin accesses dispute management section
2. System displays list of reported issues
3. Admin reviews dispute details
4. Admin communicates with involved parties
5. Admin makes decision
6. System notifies involved parties
7. System updates booking/payment status if needed

## Relationships

### Include Relationships
- "Book Property" includes "Make Payment"
- "Cancel Booking" may include "Process Refund"
- "Login to System" is required before accessing most other use cases

### Extend Relationships
- "Receive Notifications" extends many use cases (booking confirmations, payment updates, new reviews)
- "Handle Disputes" extends "Cancel Booking" in conflict situations

## System Boundary
The system boundary encompasses all the core functionality of the Airbnb Clone platform, with external systems handling specialized services like payment processing and email notifications.