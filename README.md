# IITG Travel Guide

## Overview
The **IITG Travel Guide** is a web-based platform designed for IIT Guwahati students to streamline travel planning. It offers a user-friendly interface to discover destinations, plan trips, manage budgets, and share community-driven reviews. Built as a DBMS project by Abhiram (230150015), the platform leverages modern web technologies and mapping APIs to provide dynamic features like distance calculations, route mapping, and seasonal recommendations.

This project addresses the challenges faced by IITG students in planning cost-effective and efficient trips, particularly given the institute's location in Assam. It fosters a collaborative community by allowing students to contribute reviews and share travel experiences, making it an indispensable tool for student travelers.

## Features
- **Dynamic Distance Calculator**: Calculates distances from IIT Guwahati to destinations or between consecutive destinations in a multi-stop itinerary, using the Open Source Routing Machine (OSRM) API.
- **Automated Route Mapping**: Integrates interactive maps (via Leaflet and Leaflet Routing Machine) to visualize trip itineraries and highlight nearby attractions.
- **Smart Trip Planning**: Suggests destinations based on user preferences (budget, travel duration, interests) and dynamically adjusts itineraries.
- **Community-Driven Reviews**: Allows students to submit and view authentic reviews, including ratings, comments, and travel tips for destinations.
- **Budget Management**: Estimates costs for transportation, accommodation, and food, tailored to student budgets.
- **Dynamic Trip Management**: Manages ongoing and past trips with real-time updates and archiving capabilities.
- **Contact and Feedback System**: Enables users to submit inquiries or feature requests, stored in a database for administrator review.

## Tech Stack
### Frontend
- **HTML5, CSS3, JavaScript**: Core technologies for building the user interface.
- **Bootstrap 5.3.3**: For responsive design and consistent styling.
- **AOS (Animate On Scroll)**: For smooth scroll-based animations.
- **Leaflet & Leaflet Routing Machine**: For interactive maps and route visualization.
- **Font Awesome**: For icons used throughout the interface.

### Backend
- **PHP**: Handles server-side logic, including form processing and session management.
- **MySQL**: Stores user data, trip details, destinations, and reviews.
- **OSRM API**: Provides accurate distance calculations for trip planning.

### Security
- **Password Hashing**: Uses `password_hash()` for secure password storage.
- **Prepared Statements**: Prevents SQL injection in database queries.
- **Session-Based Authentication**: Ensures secure user access to protected pages.

## Repository Structure
Below is the file and folder structure of the `IITG-Travel-Guide` repository:
```
IITG-Travel-Guide/
├── Videos/                     # Directory for video assets (e.g., nature.mp4 for homepage background)
├── config/                     # Configuration files (e.g., dbConnection.php for database settings)
├── css/                        # CSS stylesheets for the application
├── maininclude/                # Common PHP includes for shared functionality
├── output/                     # Directory for generated outputs (e.g., logs, reports)
├── user/                       # User-related scripts and pages
├── Travel_Guide.sql            # SQL dump for database schema and sample data
├── Travel_Guide_report.pdf     # Project report documenting the application
├── README.md                   # Project documentation (this file)
├── index.php                   # Homepage of the application
├── login.php                   # User login page
├── logo.png                    # Application logo
├── process_contact.php         # Script to handle contact form submissions
└── signup.php                  # User registration page
```

## Installation
### Prerequisites
- **XAMPP** (recommended): Includes Apache, MySQL, PHP, and phpMyAdmin for an all-in-one local server setup.
- PHP 7.4 or higher
- MySQL 5.7 or higher
- Internet access (for external APIs like OSRM and CDN-hosted libraries)

### Setup Instructions
1. **Install XAMPP**:
   - Download and install XAMPP from [https://www.apachefriends.org/](https://www.apachefriends.org/) for your operating system (Windows, macOS, or Linux).
   - Start the **Apache** and **MySQL** modules from the XAMPP Control Panel.

2. **Clone the Repository**:
   - Clone the project to the `htdocs` folder in your XAMPP installation directory (e.g., `C:\xampp\htdocs` on Windows or `/Applications/XAMPP/htdocs` on macOS):
     ```bash
     git clone <repository-url> iitg-travel-guide
     cd iitg-travel-guide
     ```

3. **Configure the Database**:
   - Open a browser and navigate to `http://localhost/phpmyadmin`.
   - Create a new database named `Travel_Guide`:
     - Click **New** in the left sidebar, enter `Travel_Guide` as the database name, and click **Create**.
   - Import the database schema and sample data from `Travel_Guide.sql`:
     - Select the `Travel_Guide` database, go to the **Import** tab, click **Choose File**, select `Travel_Guide.sql`, and click **Go**.
     - Alternatively, use the MySQL command line:
       ```bash
       mysql -u root -p Travel_Guide < Travel_Guide.sql
       ```
       (The default XAMPP MySQL user is `root` with no password unless changed.)

4. **Configure Database Connection**:
   - Update `config/dbConnection.php` with your database credentials. For XAMPP’s default setup, use:
     ```php
     <?php
     $host = 'localhost';
     $db = 'Travel_Guide';
     $user = 'root';
     $pass = ''; // Default XAMPP MySQL password is empty
     $conn = new mysqli($host, $user, $pass, $db);
     if ($conn->connect_error) {
         die("Connection failed: " . $conn->connect_error);
     }
     ?>
     ```

5. **Set Up File Structure**:
   - Ensure the following directories exist and are writable by Apache:
     - `Uploads/profile_images/`: For storing user profile images (create if not present).
     - `Videos/`: For video background (e.g., `nature.mp4`).
     - `images/`: For assets like `earth_texture.jpg` for the 3D globe (create if not present).
     - `output/`: For generated outputs (create this directory if not present).
   - On Windows, these permissions are usually fine by default. On macOS/Linux, set permissions if needed:
     ```bash
     chmod -R 777 Uploads/profile_images Videos images output
     ```

6. **Install Dependencies**:
   - The project uses CDN-hosted libraries (Bootstrap, Leaflet, Font Awesome, AOS). Ensure internet connectivity or host these libraries locally in the project directory if needed.

7. **Run the Application**:
   - Open a browser and access the application at `http://localhost/iitg-travel-guide`.
   - If you encounter issues, ensure Apache and MySQL are running in the XAMPP Control Panel and check the Apache error logs in `xampp/apache/logs/error.log`.

## Usage
1. **Homepage (`index.php`)**:
   - Features a video background with a 3D globe animation.
   - Provides an overview of the platform and a call-to-action for login/register.

2. **Dashboard (`dashboard.php`)**:
   - Displays user-specific information, including upcoming trips, pending reviews, and monthly destination recommendations.
   - Allows quick access to trip planning, profile editing, and trip history.

3. **Trip Planning (`plan_trip.php`)**:
   - Search and filter destinations by name, best time to visit, trip type, or maximum distance.
   - Add destinations to a current trip, view detailed destination information, and read community reviews.

4. **Current Trip (`current_trip.php`)**:
   - Manages the active trip plan with options to reorder, remove, or clear destinations.
   - Displays a route map, total distance, stay time, and estimated costs.
   - Allows trip confirmation with details like trip name, transport mode, and dates.

5. **Past Trips (`past_trips.php`)**:
   - Shows ongoing, upcoming, and completed trips with details and review options.
   - Uses `trip_card.php` for consistent trip card rendering.

6. **Trip Details (`trip_details.php`)**:
   - Displays detailed information about a specific trip, including itinerary and budget.

7. **Search Results (`search_results.php`)**:
   - Displays destinations matching the search query with details like distance, costs, and ratings.

## Security Features
- **Password Hashing**: User passwords are hashed using PHP's `password_hash()` function.
- **SQL Injection Prevention**: Uses prepared statements for all database queries.
- **Session Management**: Ensures secure user authentication and access control.

## Future Work
- **Real-Time API Integration**: Incorporate live pricing data for transportation and accommodations.
- **Machine Learning**: Implement personalized destination recommendations using ML algorithms.
- **Mobile App**: Develop a mobile version for on-the-go access.
- **Enhanced Mapping**: Add real-time traffic data and alternative route suggestions.

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m 'Add your feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

Please ensure your code follows the project's coding standards and includes appropriate documentation.


## Acknowledgments
- **Bootstrap**: For responsive UI components.
- **Leaflet & Leaflet Routing Machine**: For interactive mapping.
- **Font Awesome**: For icons.
- **AOS**: For scroll animations.
- **OSRM**: For accurate distance calculations.

For further details, refer to the project report (`Travel_Guide_report.pdf`) in the root directory.
