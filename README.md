# airbnb-clone-project

#Front-End
This project is a full-stack clone of the popular accomodation booking platform AirBnB. The goal is to build a functional web application that allows users to browse property listings, view detailed property information, and complete bookings.
Tech Stack
* Frontend: HTML,CSS,Js
* Version Control: Git and Github
* Design Tools: Figma

UI/UX Design Planning
Design Goals
* Create intuitive booking flow
* Maintain visual consistency
* Ensure fast loading times
* Prioritize mobile responsiveness

Key Features
* Property search and filtering
* Detailed property viewing
* Secure checkout process
* User authentication

Primary Pages
Page                                                Description
Property Listing View                               Grid display of available properties with filters
Listing Detailed View                               Complete property details with images and booking form
Simple Checkout View                                Streamlined payment and booking information

Importance of User-Friendly Design
A well-designed booking system reduces friction in the user journey, increases conversion rates, and improves customer satisfaction. Clear navigation, intuitive interfaces, and responsive design are critical for success.

Color Styles
* Primary: #FF5A5F
* Secondary: #008489
* Background: #FFFFFF
* Text: #222222
* Secondary Text: #717171

Typography
* Primary Font: Circular, Medium(500), 16px
* Headings: Circular, Bold(700), 24px-32px
* Secondary Text: Circular, Book (400), 14px

Project Roles and Responsibilities
Role                  Responsibilities 
Project Manager       Oversees timeline, coordinates team, manages deliverables
Frontend Developers   Implements UI components, ensures responsive design
Backend Developers    Builds APIs, manages database, implements business logic
Designers             Creates mockups, maintains design system, ensures UX quality
QA/Testers            Writes test cases, performs testing, reports bugs
DevOps Engineer       Manages deployment, CI/CD pipeline, server infrastructure
Product Owner         Defines requirements, prioritizes features, represents stakeholders
Scrum Master          Facilitates agile processes, removes blockers, organizes meetings

UI Component Patterns
* Navbar
    Logo
    Search bar
    User navigation
    Responsive menu
* Property Card
    Property image
    Basic details(price, location, rating)
    Favorite button
    Responsive layout
* Footer
    Site links
    Company information
    Social media links
    Copyright information


#Back-End
  Team Roles
* Business Analysts(BA): Understands customer’s business processes, Translates customer business needs into requirements
* Product Owner(PO):  Holds responsibility for a product vision and evolution, Makes sure the final product meets
                      customer requirements
* Project Manager:    Makes sure a product or its part is delivered on time and within budget, Manages and motivates the                        software development team
* UI/UX Designer:     Transforms a product vision into user-friendly designs, Creates user journeys for the best user                           experience and highest conversion rates
* Software Architect: Designs a high-level software architecture, Selects appropriate tools and platforms to implement                          the product vision, Sets up code quality standards and performs code reviews
* Software Developer: Engineers and stabilizes the product, Solves any technical problems emerging during the development                       lifecycle
* Quality Assurance (QA) Engineer: Makes sure an application performs according to requirements, Spots functional and                                        non-functional defects
* Test Automation Engineer: Designs a test automation ecosystem, Writes and maintains test scripts for automated testing
* DevOps Engineer: Facilitates cooperation between development and operations teams, Builds continuous integration and                       continuous delivery (CI/CD) pipelines for faster delivery

Technology Stack
Django: A high-level Python web framework used to build the backend server and RESTful APIs. It provides the core structure for the application (models, views, URL routing, admin interface) and handles security, database interaction, and server logic.

PostgreSQL: A powerful, open-source relational database system. It is used as the primary data storage for the application, securely storing and managing all structured data like user accounts, content, and transactional information.

GraphQl: A query language for APIs and a runtime for fulfilling those queries with your existing data. It allows the frontend client to request exactly the data it needs in a single request, preventing over-fetching or under-fetching of data common in REST APIs.

Database Design
* User
  Purpose:Represents all individuals using the platform, both property owners/hosts and guests.
  Important Fields:
      1. id (Primary Key): A unique identifier.
      2. email: For authentication and communication.
      3. first_name & last_name: For personalization and identification.
  Relationship
      1. A User (as a host) can have many Properties (One-to-Many).
      2. A User (as a guest) can have many Bookings (One-to-Many).
      3. A User can have many Reviews (both as a author reviewing a property and as a recipient             being reviewed) (One-to-Many).
* Properties
  Purpose:  Represents a rental unit or space listed by a host.
  Important Fields
      1. id (Primary Key): A unique identifier.
      2. title: A name for the listing.
      3. description: Details about the property.
      4. price_per_night: The cost to book for one night.
      5. host_id (Foreign Key): Links the property to its owner.
  Relationship
      1. A Property belongs to one User (the host) (Many-to-One).
      2. A Property can have many Bookings (One-to-Many).
      3. A Property can have many Reviews (One-to-Many).
      4. A Property can have many Amenities and an Amenity can be on many Properties (Many-to-            Many).
  * Bookings
    Purpose: Represents a reservation where a guest books a property for a specific time period.
    Important Fields
        1. id (Primary Key): A unique identifier.
        2. start_date: The check-in date.
        3. end_date: The check-out date.
        4. total_price: The calculated cost for the stay.
        5. guest_id (Foreign Key): Links to the User who made the booking.
        6. property_id (Foreign Key): Links to the Property being booked.
    Relationship
        1. A Booking belongs to one User (the guest) (Many-to-One).
        2. A Booking belongs to one Property (Many-to-One).
        3. A Booking can have one Payment (One-to-One).

    *Reviews
        Purpose: Allows guests to leave feedback on a property and for hosts to review guests
        after a stay.
        Important Fields
            1. id (Primary Key): A unique identifier.
            2. rating: A numerical score (e.g., 1-5 stars).
            3. comment: The written feedback.
            4. author_id (Foreign Key): Links to the User writing the review.
            5. recipient_id (Foreign Key): Links to the User being reviewed (if for a guest).
            6. property_id (Foreign Key): Links to the Property being reviewed.
        Relationship
            1. A Review belongs to one User (as the author) (Many-to-One).
            2. A Review can belong to one User (as the recipient, for guest reviews) (Many-to-                 One - Optional).
            3. A Review belongs to one Property (for property reviews) (Many-to-One).
            4.A Review can belong to one Booking (to ensure only guests with completed stays                   can review) (One-to-One).
    *Payments
        Purpose: Records the financial transaction associated with a booking.
        Important Fields
            1. id (Primary Key): A unique identifier.
            2. amount: The total amount paid.
            3. currency: The currency of the payment (e.g., USD, EUR).
            4. payment_intent_id: ID from the payment processor (e.g., Stripe).
            5. status: The status of the payment (e.g., succeeded, failed, refunded).
            6. booking_id (Foreign Key): Links the payment to a specific booking.
        Relationship
            1. A Payment belongs to one Booking (One-to-One).

    Feature Breakdown
    * User Management: This feature allows users to securely register, log in, and manage their                         profiles. It forms the foundation of the platform by protecting user                            data and providing a personalized experience for both guests and hosts.
    * Property Management: This enables hosts to create, update, and manage detailed listings                            for their properties, including descriptions, photos, prices, and                               availability. It is the core inventory of the platform, providing                               guests with options to browse and book.
    * Boooking System: This system handles the entire lifecycle of a reservation, from checking                         availability and calculating costs to confirming and managing bookings.                         It is the primary transaction engine of the platform, facilitating the                          core service of connecting guests with hosts.


    API Security
        * Authentication
        Measures: Implementation of a robust system using hashed and salted                             passwords (with algorithms like bcrypt), JWT (JSON Web Tokens) for stateless session            management, and secure password reset flows.
        Why it's Crucial: This is the first line of defense. Strong authentication ensures              that only legitimate users can access their accounts, preventing unauthorized access            to personal data, financial information, and private messages.

    * Authorization:
          Measures: Implementing role-based access control (RBAC) and object-level permissions            (e.g., ensuring a user can only edit their own property listings, profile, and                  bookings).
          Why it's Crucial: Authorization defines what authenticated users are allowed to do.             It is critical for preventing users from accessing or modifying data that isn't                 theirs (e.g., a guest canceling another user's booking or a host deleting a review),            which protects user privacy and data integrity.
    * Rate Limiting
          Measures: Implementing limits on how often an API endpoint or authentication route              can be called from a single IP address/user account within a specific time window               (e.g., using Django Ratelimit or Django REST Framework's throttling classes).
          Why it's Crucial: This protects the application from Denial-of-Service (DoS) and                brute-force attacks. It prevents bots from overwhelming the login system with                   countless password guesses or from scraping the entire property database, ensuring              service availability for legitimate users.
      *Payment Security
          Measures: Never storing raw credit card details. Using a certified payment processor            (e.g., Stripe, Braintree) and relying on their APIs and tokens (like PaymentIntent              IDs) to handle transactions. Ensuring all payment flows are over HTTPS.
          Why it's Crucial: This is non-negotiable for handling financial data. A breach here             would lead to direct financial fraud, devastating legal liability, and a complete               loss of user trust. Compliance with standards like PCI DSS is mandatory.

      CI/CD Pipeline
          CI/CD (Continuous Integration and Continuous Deployment/Delivery) is an automated               process that helps developers reliably build, test, and deploy software.
          Continuous Integration (CI): The practice of automatically building and testing code            every time a developer pushes a change to the shared repository (e.g., on GitHub).              This ensures new code integrates smoothly and doesn't break the existing application.
          Continuous Deployment/Delivery (CD): The automated process of deploying the                     successfully tested code from the CI stage directly to a staging or production                  server. This allows for frequent and reliable releases.

      * Why are they important for this project?
        1.  Improves Code Quality & Stability: Automated testing in the CI pipeline catches                 bugs and regressions before they reach users, leading to a more stable and reliable             booking platform.
        2.  Enables Rapid & Safe Deployments: CD automates the deployment process, allowing you             to release new features, security patches, and bug fixes quickly and consistently               with minimal manual effort, reducing the risk of human error.
        3. Increases Team Productivity: Automation frees developers from manual testing and                deployment tasks, allowing them to focus on building new features. It also provides             immediate feedback on their code changes.

       * Tools That Could Be Used
             GitHub Actions
             Docker
             AWS CodeDeploy
         











