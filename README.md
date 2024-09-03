# IRCTC-like Railway Management System API

This project implements a Railway Management System API similar to IRCTC using PHP and MySQL, allowing users to check train availability, book seats, and manage train information.

## Features

- User registration and authentication
- Train information management (admin only)
- Real-time seat availability checking
- Seat booking with race condition handling
- Booking details retrieval
- Role-based access control (Admin and Login users)

## Tech Stack

- Backend: PHP
- Database: MySQL
- Web Server: Apache (recommended)

## Prerequisites

- PHP (Version 7.4 or 8.1 recommended)
- MySQL 5.7+
- Apache web server
- Composer (for dependency management)

## Setup

1. Clone the repository:
   ```
   git clone https://github.com/your-username/railway-management-api.git
   cd railway-management-api
   ```

2. Install dependencies:
   ```
   composer install
   ```

3. Set up the database:
   - Create a new MySQL database for the project
   - Import the provided SQL file: `database/railway_management.sql`

4. Configure the application:
   - Copy `.env.example` to `.env`
   - Update the `.env` file with your database credentials and API key

5. Set up your web server:
   - Configure Apache to point to the `public` directory of the project
   - Ensure mod_rewrite is enabled for routing

## Running the Application

1. Start your Apache server and MySQL service
2. Access the API at `http://localhost/railway-management-api/public`

## API Endpoints

1. `POST /api/register`: Register a user
2. `POST /api/login`: Login user
3. `POST /api/admin/trains`: Add a new train (Admin only)
4. `GET /api/trains`: Get seat availability between source and destination
5. `POST /api/bookings`: Book a seat on a train
6. `GET /api/bookings/{booking_id}`: Get specific booking details

## Authentication

- Admin endpoints are protected with an API key (set in the `.env` file)
- User endpoints require a JWT token obtained from the login endpoint

## Testing

To run the test suite:

```
vendor/bin/phpunit
```

## Race Condition Handling

To handle race conditions during simultaneous booking attempts:

1. We use database transactions to ensure data consistency
2. Implement row-level locking when updating seat availability
3. If multiple users try to book the last seat simultaneously, only one booking will succeed

## Assumptions

1. Each train has a fixed number of seats for the entire journey
2. Booking is done for the entire journey from source to destination
3. The admin API key is stored securely in the `.env` file
4. JWT tokens have a reasonable expiration time for security

## Development Notes

- This project was developed within a 24-hour timeframe as per the given requirements
- The API is designed to handle high traffic and optimized for performance
- All code is original and developed without the use of AI code generation tools

## License
This project is licensed under the MIT License - see the LICENSE.md file for details.
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
