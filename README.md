# Smart Event Management System - Backend

A comprehensive Spring Boot REST API backend for managing events, attendees, and providing intelligent recommendations. This is a production-ready application suitable for portfolio and resume purposes.

## 🎯 Project Overview

The Smart Event Management System is a full-featured backend application that solves the problem of event discovery, management, and attendee coordination. It provides:

- **Event Management**: Create, update, and manage events
- **User Management**: User registration and profile management
- **RSVP System**: Attendee tracking and check-in management
- **Review & Ratings**: Community feedback on events
- **Smart Recommendations**: AI-driven event suggestions based on user interests and location
- **Search & Filter**: Advanced search capabilities across events and users

## 🏗️ Technology Stack

- **Framework**: Spring Boot 3.1.5
- **Language**: Java 17
- **ORM**: Hibernate with Spring Data JPA
- **Database**: MySQL 8.0 (H2 for testing)
- **Build Tool**: Maven
- **Additional Libraries**:
  - Lombok (for reducing boilerplate)
  - MapStruct (for object mapping)
  - Validation (Jakarta Bean Validation)

## 📋 Features

### User Management
- User registration and profile creation
- User search and filtering by city
- Update user profiles
- Soft delete functionality

### Event Management
- Create and manage events
- Event categorization
- Search events by title, description, or location
- Filter by category and city
- Update event status (UPCOMING, ONGOING, COMPLETED, CANCELLED)
- Public/Private event settings

### RSVP & Attendee Management
- RSVP to events with status (ATTENDING, INTERESTED, NOT_ATTENDING, MAYBE)
- Track number of guests
- Check-in functionality with timestamps
- View attendee lists by status

### Reviews & Ratings
- 5-star rating system
- Write event reviews
- View event average ratings
- Mark helpful reviews
- User review history

### Smart Recommendations
- Personalized event recommendations based on:
  - User location (city)
  - User interests
  - Event ratings and popularity
- Sorted by relevance and quality

## 🚀 Getting Started

### Prerequisites
- Java 17 or higher
- Maven 3.8+
- MySQL 8.0+

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/sriramtenneti03/Java-Backend.git
cd Java-Backend
```

2. **Create MySQL Database**
```sql
CREATE DATABASE event_management;
```

3. **Update Database Configuration**
Edit `src/main/resources/application.yml`:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/event_management
    username: root
    password: your_password
```

4. **Build the project**
```bash
mvn clean install
```

5. **Run the application**
```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## 📡 API Endpoints

### User Endpoints
- `POST /api/users/register` - Register a new user
- `GET /api/users/{id}` - Get user by ID
- `GET /api/users/email/{email}` - Get user by email
- `GET /api/users` - Get all active users
- `GET /api/users/search?keyword=xyz` - Search users
- `GET /api/users/city/{city}` - Get users by city
- `PUT /api/users/{id}` - Update user profile
- `DELETE /api/users/{id}` - Delete user (soft delete)

### Event Endpoints
- `POST /api/events` - Create event (requires organizerId)
- `GET /api/events/{id}` - Get event by ID
- `GET /api/events/upcoming` - Get upcoming public events
- `GET /api/events/category/{category}` - Get events by category
- `GET /api/events/city/{city}` - Get events by city
- `GET /api/events/organizer/{organizerId}` - Get events by organizer
- `GET /api/events/search?keyword=xyz` - Search events
- `GET /api/events/recommendations?userId={id}` - Get personalized recommendations
- `PUT /api/events/{id}` - Update event
- `PATCH /api/events/{id}/status?status=COMPLETED` - Update event status
- `DELETE /api/events/{id}` - Delete event

### RSVP/Attendee Endpoints
- `POST /api/attendees/rsvp` - RSVP to event
- `DELETE /api/attendees/cancel-rsvp` - Cancel RSVP
- `GET /api/attendees/event/{eventId}` - Get event attendees
- `GET /api/attendees/event/{eventId}/status/{status}` - Get attendees by status
- `GET /api/attendees/user/{userId}` - Get user's attending events
- `GET /api/attendees/count/{eventId}` - Get attendee count
- `POST /api/attendees/{attendeeId}/check-in` - Check in attendee

### Review Endpoints
- `POST /api/reviews` - Create review
- `GET /api/reviews/event/{eventId}` - Get event reviews
- `GET /api/reviews/user/{userId}` - Get user reviews
- `GET /api/reviews/event/{eventId}/average-rating` - Get event average rating
- `GET /api/reviews/event/{eventId}/count` - Get review count
- `PUT /api/reviews/{reviewId}` - Update review
- `DELETE /api/reviews/{reviewId}` - Delete review
- `POST /api/reviews/{reviewId}/mark-helpful` - Mark review as helpful

## 📊 Database Schema

### Users Table
- Stores user information including email, profile, interests
- Soft delete using `is_active` flag

### Events Table
- Event information created by users
- Supports public/private events
- Status tracking (UPCOMING, ONGOING, COMPLETED, CANCELLED)

### Attendees Table
- Tracks RSVP status of users to events
- Check-in functionality
- Number of guests tracking
- Unique constraint on (event_id, user_id)

### Reviews Table
- Event reviews and ratings
- Author tracking
- Helpful count functionality

## 🧪 Testing

Run tests with:
```bash
mvn test
```

## 📝 Sample Request/Response

### Create User
```bash
curl -X POST http://localhost:8080/api/users/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "fullName": "John Doe",
    "password": "password123",
    "city": "New York",
    "interests": "Technology, Music, Networking"
  }'
```

### Create Event
```bash
curl -X POST "http://localhost:8080/api/events?organizerId=1" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Java Spring Boot Meetup",
    "description": "Learn Spring Boot best practices",
    "category": "Technology",
    "eventDate": "2024-06-15T18:00:00",
    "location": "Tech Hub, Downtown",
    "city": "New York",
    "maxAttendees": 50
  }'
```

## 🔄 Architecture

```
com.eventmanagement/
├── entity/          # JPA entities
├── dto/            # Data Transfer Objects
├── repository/     # Spring Data JPA repositories
├── service/        # Business logic layer
├── controller/     # REST API controllers
├── exception/      # Custom exceptions
└── config/         # Spring configuration
```

## 🎓 Key Learning Points

This project demonstrates:

1. **Spring Boot Best Practices**
   - Proper layering (Controller → Service → Repository)
   - Dependency injection
   - Transaction management

2. **Hibernate & JPA**
   - Entity relationships
   - Custom queries
   - Database initialization

3. **REST API Design**
   - Proper HTTP methods and status codes
   - Request validation
   - Global exception handling
   - DTO pattern

4. **Business Logic**
   - Smart recommendations algorithm
   - RSVP management
   - Review aggregation

5. **Database Design**
   - Normalized schema
   - Proper indexing
   - Soft delete pattern

## 🚀 Future Enhancements

- Authentication & Authorization (JWT)
- Email notifications
- Advanced analytics
- Mobile app support
- Image upload functionality
- Event categories and tags
- Ticketing system
- Payment integration
- Real-time notifications using WebSockets

## 📞 Contact

For questions or suggestions, feel free to reach out!

## 📄 License

This project is open source and available under the MIT License.