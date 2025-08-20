# airbnb-clone-project

The Airbnb Clone Project is a comprehensive, real-world application designed to simulate the development of a robust booking platform like Airbnb. It involves a deep dive into full-stack development, focusing on backend systems, database design, API development, and application security. This project enables learners to understand complex architectures, workflows, and collaborative team dynamics while building a scalable web application.

Modern tools-Docker, Github Actions and other similar CI/CD platforms.

Team Roles
>Backend Developer
They implement the core of an app, its algorithms and business logic. They also devise the app architecture or design and implement the necessary integrations.
>Database Administrator
They manage databases by designing the schema, availing test data, providing staging databases for tests before going live.
>DevOps Engineer
Builds continuous integration and continuous delivery (CI/CD) pipelines for faster delivery
>UI Designer
They translate the product vision into user-friendly designs. Basically designs the interfaces for the airbnb-clone-project.
>UX Designer
Is involved in user research, persona development, information structure design, wireframing, prototyping as they think out the entire journey of a user's interaction with the airbnb-clone-project.

Technology Stack
Django, MySQL, GraphSQL, PostgreSQL.
>Django
This is the web framework to be used to handle logic and connects everything.
It handles user authentication, manages business logic, provides Django ORM for database queries without raw SQL, includes security features and comes with an admin dashboard.
>MySQL
It will serve as the main database for storing structured data for example user profiles, listings, bookings etc
>GraphSQL
It will be used to fetch and manipulate data from the backend in a flexible way instead of traditional REST APIs.
>PostgreSQL
Also a relational database that's often chosen for complex queries, scalability and advanced features. It handles geospatial quesries, supports JSON fields and more robust with data integrity and transactions.

Database Design
Key Entities
User Profiles, Properties, Bookings, Reviews and Payments
1. Users Profiles (Guests & Hosts)

id (Primary Key)
name (full name of the user)
email (unique login identifier)
role (guest, host, or admin)
date_joined (when the user signed up)

>User-Properties
--one property belongs to exactly one host(user)
--many properties can belong to one host(user)
>User-Bookings
--One guest (User) can make many bookings.
--One booking belongs to exactly one guest(user).
>Users-Reviews
--One guest (User) can write many reviews.
--One review belongs to exactly one guest.

2. Properties (Listings)

id (Primary Key)
user_id (host_id) (FK → Users, the host who owns this property)
title (“Cozy Apartment in Nairobi”)
location (address or coordinates)
price_per_night (numeric)
status (available, booked, inactive)

>User-Properties
--one property belongs to exactly one host(user)
--many properties can belong to one host(user)
>Properties-Bookings
--One property can have many bookings(over time)
--One booking is linked to exactly one property
>Properties-Reviews
--One property can have many reviews.
--One review is tied to exactly one property.

3. Bookings

id (Primary Key)
property_id (FK → Properties)
user_id (guest_id) (FK → Users, the person booking)
check_in_date
check_out_date
status (pending, confirmed, cancelled)

>Properties-Bookings
--One property can have many bookings(over time)
--One booking is linked to exactly one property
>Bookings-Payments
--One booking has one payment record.
--One payment is tied to exactly one booking.

4. Reviews

id (Primary Key)
property_id (FK → Properties)
user_id (guest_id) (FK → Users, reviewer)
rating (1–5 stars)
comment (text)
created_at (timestamp)

>Users-Reviews
--One guest (User) can write many reviews.
--One review belongs to exactly one guest.
>Properties-Reviews
--One property can have many reviews.
--One review is tied to exactly one property.

5. Payments

id (Primary Key)
booking_id (FK → Bookings)
amount (numeric)
payment_method(card, mobile money,PayPal)
payment_date (timestamp)
status (pending, completed, failed, refunded)

>Bookings-Payments
--One booking has one payment record.
--One payment is tied to exactly one booking.

Feature Breakdown
>User Management 
 Secure guest and host accounts with registration, login, and profile management. This builds the foundation of trust, ensuring users can manage their details and interact safely on the platform.

>Property Management
Hosts can list, update, and manage properties with information such as location, pricing, and amenities. This allows for a wide range of accommodation options and gives hosts full control over their listings.

>Booking System
Guests can search, select, and book properties based on availability and dates. The system prevents double bookings and manages reservations, ensuring a smooth guest–host experience.

>Reviews and Ratings
Guests can leave reviews and rate properties after their stay. This promotes transparency, helps future guests make informed choices, and provides feedback for hosts to improve.

>Payments
Securely processes payments for bookings, handling statuses such as pending, confirmed, or refunded. This adds reliability and ensures safe transactions for both hosts and guests.

API Security
>Authentication
Verifies user identity during login using secure methods for example email/password, OAuth, or two-factor authentication.  
Crucial for preventing unauthorized access and protecting user accounts.

>Authorization
Ensures users only access features and data relevant to their role (e.g. hosts manage their own properties, guests manage their bookings).  
This prevents data leaks and enforces role-based access control.

>Data Encryption 
All sensitive data is encrypted both in transit (via HTTPS/TLS) and at rest (database-level encryption).  
This protects personal details, login credentials, and financial data from interception or theft.

>Secure Payments
Payments are handled through trusted gateways (e.g. PayPal, or M-Pesa API) using tokenization and PCI-DSS compliance.  
This ensures transactions are secure and minimizes fraud risks.

>Input Validation & Sanitization
User inputs are validated and sanitized before being processed.  
This prevents injection attacks such as SQL injection or XSS, safeguarding the database and frontend.

>Rate Limiting & Throttling
Controls the number of requests per user or IP within a set timeframe.  
This defends against brute force attacks, spam, and DDoS attempts.

>Logging & Monitoring
Tracks login attempts, unusual activity, and system errors in real-time.  
This enables quick detection and response to potential security breaches.

>Double Booking Prevention
The booking system uses database transactions and availability checks at both the search and confirmation stages.  
This ensures two guests cannot reserve the same property for overlapping dates.

>Double Payment Prevention
Each booking is tied to a single payment record using idempotency keys and one-to-one booking–payment mapping.  
This prevents users from being charged multiple times due to retries or repeated clicks.

CI/CD Pipeline
CI/CD (Continuous Integration and Continuous Deployment/Delivery) pipelines automate the process of building, testing, and deploying the application.
They are important because they:
Ensure code changes are tested automatically, reducing bugs and errors.
Monitoring and logging can be integrated to catch issues in real time after deployment.
Rollback mechanisms in CI/CD allow quick recovery if something goes wrong during deployment.
Speed up deployment, making new features and fixes available faster.
Provide consistency, so every deployment follows the same reliable process.

Tools we can use:
GitHub Actions – for automated testing, linting, and deployments directly from the repository.
Docker and Kurbenetes – for containerizing and scaling the app to ensure it runs the same way in all environments.
Jenkins / GitLab CI – alternatives for advanced automation and deployment workflows.
Heroku / AWS / GCP – cloud platforms to host and deploy the application. (AWS CodePipeline, AzureDevOPs or Google Cloud for cloud-native CI/CD)
