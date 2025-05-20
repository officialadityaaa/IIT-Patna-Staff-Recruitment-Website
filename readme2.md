## Project Overview

This project is a comprehensive staff recruitment portal designed and developed for IIT Patna. It facilitates the entire faculty application process online. Key features include:

*   **User Registration & Authentication:** Secure signup and login functionality for applicants.
*   **Multi-Page Application Form:** An extensive form capturing detailed information from applicants, including personal data, educational qualifications, work experience, publications, and references.
*   **Document Uploads:** Allows applicants to upload necessary documents like CVs, certificates, and photographs, which are stored securely on Cloudinary.
*   **Password Reset:** Enables users to reset their passwords via email verification.
*   **Application Preview & Print:** Applicants can preview their complete application and print it for their records.

## Technologies Used

The project leverages a modern stack of technologies to deliver its functionalities:

*   **Backend:**
    *   **Node.js:** JavaScript runtime environment for server-side logic.
    *   **Express.js:** Web application framework for Node.js, used for building robust APIs and handling routing.
*   **Database:**
    *   **MySQL:** Relational database management system for storing all application data.
*   **Frontend:**
    *   **EJS (Embedded JavaScript templates):** Templating language used to generate HTML markup with plain JavaScript.
    *   **EJS-Mate:** Layout and partial template support for EJS.
*   **Authentication:**
    *   **Passport.js (with `passport-local` strategy):** Authentication middleware for Node.js, handling user login.
    *   **bcrypt:** Library for hashing passwords.
    *   **express-session:** Middleware for session management.
*   **File Uploads:**
    *   **Multer:** Middleware for handling `multipart/form-data`, primarily used for uploading files.
    *   **Cloudinary:** Cloud-based image and video management service, used for storing uploaded documents.
*   **Email Notifications:**
    *   **Nodemailer:** Module for Node.js applications to allow easy email sending (e.g., for password resets).
*   **Containerization:**
    *   **Docker:** Platform for developing, shipping, and running applications in containers.
*   **Environment Management:**
    *   **dotenv:** Module to load environment variables from a `.env` file.

## Project Structure

The project is organized into several key directories and files:

```
.
├── project 1/
│   ├── index.mjs           # Main application entry point, server setup, route definitions, database initialization.
│   ├── views/              # Contains EJS templates for different application pages.
│   │   ├── formpages/      # EJS templates for the multi-page application form.
│   │   ├── home/           # EJS templates for homepage, login, signup.
│   │   └── layout/         # EJS layout files (e.g., for common headers/footers).
│   ├── public/             # Static assets accessible by the client.
│   │   ├── css/            # Stylesheets for the application.
│   │   ├── javascript/     # Client-side JavaScript files.
│   │   └── assets/         # Images and other static assets.
│   ├── package.json        # Lists project dependencies and scripts.
│   ├── package-lock.json   # Records exact versions of dependencies.
│   ├── dockerfile          # Instructions to build the Docker image for the application.
│   ├── docker-compose.yml  # Defines and configures the Docker services (application).
│   └── ...                 # Other files and folders within project 1
├── README.md               # Original README file with basic setup instructions.
└── readme2.md              # This detailed documentation file.
```

*   **`project 1/index.mjs`**: This is the heart of the application. It initializes the Express server, connects to the MySQL database, defines all the application routes (including authentication and form pages), sets up middleware (like body-parser, session management, Passport.js), and handles application logic. It also includes the SQL queries for creating the necessary database tables if they don't already exist.
*   **`project 1/views/`**: This directory holds all the EJS (`.ejs`) template files. EJS is used to render dynamic HTML content by embedding JavaScript.
    *   `formpages/`: Contains the individual EJS files for each step of the multi-page faculty application form.
    *   `home/`: Includes templates for user-facing pages like the login screen, signup page, and potentially a landing page.
    *   `layout/`: Contains reusable layout templates, such as `every.ejs`, which defines the common structure (headers, footers, etc.) for most application pages.
*   **`project 1/public/`**: This directory serves static files directly to the client's browser.
    *   `css/`: Contains CSS files for styling the application.
    *   `javascript/`: Holds client-side JavaScript files for interactive features.
    *   `assets/`: Stores images, fonts, or other static resources.
*   **`project 1/package.json`**: Standard Node.js manifest file that lists project metadata, dependencies (libraries required by the project), and devDependencies (libraries for development).
*   **`project 1/dockerfile`**: A script containing instructions for building a Docker image of the application. This ensures that the application runs in a consistent environment.
*   **`project 1/docker-compose.yml`**: A YAML file used to define and run multi-container Docker applications. In this case, it likely defines the Node.js application service, specifying the build context, image name, port mappings, and volume mounts.

## Database Schema

The application uses a MySQL database to store user information, application details, and related data. The tables are automatically created if they don't exist when the application starts. The primary key for most tables is an auto-incrementing `id`, and `email` is commonly used as a foreign key or an identifier to link data across tables for a specific user.

Here's a summary of the tables:

*   **`users`**: Stores user authentication details.
    *   `id`: Primary Key.
    *   `email`: User's email (unique, used for login).
    *   `password`: Hashed password.
*   **`profile`**: Stores basic profile information created during signup.
    *   `id`: Primary Key.
    *   `first_name`, `last_name`: User's name.
    *   `category`: User's category.
    *   `email`: User's email.
*   **`applicationdetails`**: Stores details related to a specific job application.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   `adv_num`, `doa`, `app_num`, `post`, `dept`: Advertisement number, date of application, application number, post applied for, and department.
*   **`personaldetails`**: Stores detailed personal information of the applicant.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Includes fields for name, nationality, DOB, gender, marital status, category, ID proof details, father's name, addresses, and contact numbers.
    *   `image_path`, `idproof_image`: Paths to uploaded photo and ID proof (likely Cloudinary URLs).
*   **`educationaldetails`**: Stores academic qualifications from PhD down to SSC/SSC.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Includes fields for PhD, PG, UG, HSC (12th), and SSC (10th) details like college, stream, year, marks, etc.
*   **`edu_additionaldetails`**: Stores any additional academic qualifications or courses.
    *   `id`: Primary Key.
    *   `educationaldetails_id`: Foreign Key referencing `educationaldetails(id)`.
    *   Fields for degree, college, subjects, year, duration, percentage, division.
*   **`publications`**: Summary of applicant's publications.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for counts of different types of publications (international/national journals/conferences, patents, books, book chapters).
*   **`top10publications`**: Details of the applicant's top 10 publications.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for author, title, journal, year, impact factor, DOI, status.
*   **`patents`**: Details of patents held by the applicant.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for author, title, country, patent number, filing/publication/issue years.
*   **`books`**: Details of books authored by the applicant.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for author, title, year, ISBN.
*   **`book_chapters`**: Details of book chapters authored by the applicant.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for author, title, year, ISBN.
*   **`googlelink`**: Stores the applicant's Google Scholar profile link (or similar).
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   `googlelink`: URL to the profile.
*   **`presentemployment`**: Details of the applicant's current employment.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for position, employer, status, DOJ, DOL, duration.
*   **`employmenthistory`**: Details of past employment.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for position, employer, DOJ, DOL, duration. (Repeated for multiple entries)
*   **`teachingexp`**: Details of teaching experience.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for position, employer, course taught, level (UG/PG), number of students, DOJ, DOL, duration. (Repeated for multiple entries)
*   **`researchexp`**: Details of research experience.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for position, institute, supervisor, DOJ, DOL, duration. (Repeated for multiple entries)
*   **`industrialexp`**: Details of industrial experience.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for organization, work profile, DOJ, DOL, duration. (Repeated for multiple entries)
*   **`aos_aor`**: Stores Areas of Specialization and Areas of Research.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   `area_spl`, `area_rese`: Text fields for specialization and research areas.
*   **`membership`**: Details of professional memberships.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for society name, membership status. (Repeated for multiple entries)
*   **`training`**: Details of professional trainings attended.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for training type, organization, year, duration. (Repeated for multiple entries)
*   **`awards`**: Details of awards and recognitions received.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for award name, awarding body, year. (Repeated for multiple entries)
*   **`sponsoredprojects`**: Details of sponsored projects undertaken.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for sponsoring agency, project title, amount, period, role, status. (Repeated for multiple entries)
*   **`consultancyprojects`**: Details of consultancy projects undertaken.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for organization, title, grant amount, period, role, status. (Repeated for multiple entries)
*   **`phd_thesis`**: Details of PhD theses supervised.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for student name, thesis title, role, status, year. (Repeated for multiple entries)
*   **`pg_thesis`**: Details of PG theses supervised.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for student name, thesis title, role, status, year. (Repeated for multiple entries)
*   **`ug_thesis`**: Details of UG theses supervised.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for student name, thesis title, role, status, year. (Repeated for multiple entries)
*   **`page_7`**: Stores longer text-based inputs like research and teaching statements.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Fields for research statement, teaching statement, relevant information, professional service, journal details, conference details.
*   **`page_8_upload`**: Stores paths to various uploaded documents for page 8 of the form.
    *   `id`: Primary Key.
    *   `email`: Applicant's email.
    *   Contains paths (likely Cloudinary URLs) for PhD certificate, PG/UG documents, 12th/10th certificates, pay slip, NOC/undertaking, post-PhD experience documents, miscellaneous certificates, best paper, and signature.
*   **`datapage`**: Stores details of references provided by the applicant. (Seems to correspond to Page 8 referees)
    *   `id`: Primary Key.
    *   `email`: Applicant's email (who is filling the form).
    *   `email07`: Email of the referee.
    *   Fields for referee's name, phone, position, association with referee, organization. (This table can store multiple referee records for each user).

This schema is quite extensive, reflecting the detailed nature of a faculty recruitment application.

## Setup and Installation

The primary method for setting up and running this project is by using Docker.

### Prerequisites

*   **Docker:** Ensure Docker Desktop or Docker Engine is installed and running on your machine. You can verify by running `docker -v`.

### Running the Application with Docker

The original `README.md` provides instructions for pulling and running a pre-built Docker image from Docker Hub.

1.  **Pull the Docker Image:**
    ```bash
    docker pull adityaboudh/iit-patna-recruit
    ```
    This command downloads the official image for the application.

2.  **Run the Docker Container:**
    When running the image, you'll need to map a host port (e.g., 8000) to the container's port 8000.
    ```bash
    # Example:
    docker run -p 8000:8000 adityaboudh/iit-patna-recruit
    ```
    Refer to the Docker Desktop interface or Docker CLI commands to manage containers. The application will be accessible at `http://localhost:8000`.

### Running with Local Code (using `docker-compose.yml`)

If you have the source code and want to run it locally, potentially with your own modifications:

1.  **Clone the Repository:**
    ```bash
    # If you haven't already
    git clone <repository_url>
    cd <repository_directory>
    ```

2.  **Configure Environment Variables:**
    The application uses a `.env` file in the `project 1/` directory to manage sensitive information and configurations. Create a file named `.env` inside the `project 1/` directory with the following content:

    ```env
    # Server Configuration
    NODE_ENV=development # or production
    SECRET=your_session_secret_here # A long, random string for session encryption

    # MySQL Database Connection
    SQL_HOST=your_mysql_host # e.g., localhost or a remote DB host
    SQL_USER=your_mysql_user
    SQL_PASSWORD=your_mysql_password
    SQL_DATABASE=your_mysql_database_name

    # Cloudinary Configuration (for file uploads)
    CLOUD_NAME=your_cloudinary_cloud_name
    CLOUD_API_KEY=your_cloudinary_api_key
    CLOUD_API_SECRET=your_cloudinary_api_secret

    # Nodemailer Configuration (for password reset emails)
    # Example for Gmail - ensure you have "less secure app access" enabled or use an app password
    EMAIL_USER=your_email_address@gmail.com
    EMAIL_PASS=your_email_password_or_app_password
    ```
    **Important Security Note:**
    *   Do NOT commit the actual `.env` file with your sensitive credentials to version control. Add `.env` to your `.gitignore` file.
    *   Replace placeholder values (like `your_mysql_host`, `your_session_secret_here`, etc.) with your actual configuration details.
    *   For `EMAIL_PASS` with Gmail, it's highly recommended to use an "App Password" if you have 2-Step Verification enabled on your Google account, rather than your main Google account password.

3.  **Build and Run with Docker Compose:**
    Navigate to the `project 1/` directory (where `docker-compose.yml` is located) and run:
    ```bash
    docker-compose up --build
    ```
    This command will:
    *   Build the Docker image for the Node.js application based on the `dockerfile` (if the image doesn't exist or if changes are detected).
    *   Start the application container as defined in `docker-compose.yml`.
    The application should then be accessible at `http://localhost:8000`. The `docker-compose.yml` is configured to mount the local code into the container, so changes to the code should be reflected automatically (you might need to restart the container or nodemon will handle it if configured).

### Database Setup

*   The application attempts to create the necessary tables automatically upon startup (as seen in `index.mjs` with `CREATE TABLE IF NOT EXISTS` statements).
*   Ensure your MySQL server is running and accessible with the credentials provided in the `.env` file.
*   You might need to create the database specified in `SQL_DATABASE` manually before starting the application if it doesn't already exist.

## Application Flow

The IIT Patna Staff Recruitment Portal guides users through a structured process from registration to application submission.

1.  **Signup (`/signup`):**
    *   New users register by providing their first name, last name, category (e.g., General, OBC, SC/ST), email address, and a password.
    *   A CAPTCHA is used for verification.
    *   Upon successful registration, user credentials (hashed password) are stored in the `users` table, and basic profile information is stored in the `profile` table.
    *   Users are typically redirected to the login page after signup.

2.  **Login (`/login`):**
    *   Registered users log in using their email and password.
    *   Passport.js (`local` strategy) handles authentication by verifying credentials against the `users` table.
    *   Upon successful login, a session is established, and users are redirected to the first page of the application form (`/formpages/1`).
    *   Failed login attempts redirect the user back to the login page.

3.  **Password Reset:**
    *   **Forgot Password (`/reset`):** If a user forgets their password, they can initiate a reset process by entering their registered email address.
    *   The system generates a unique token and sends a password reset link to the user's email via Nodemailer.
    *   **Reset Password Form (`/reset-password/:token`):** Clicking the link in the email takes the user to a form where they can enter and confirm their new password.
    *   The system updates the user's password in the `users` table after verifying the token and matching new passwords.

4.  **Multi-Page Application Form (`/formpages/1` through `/formpages/9`):**
    *   This is the core of the application, where logged-in users fill out their recruitment form. Each page corresponds to a specific section of information and has its own GET route to display the form and POST route to submit data.
    *   **Page 1 (`/formpages/1`):** Application details (advertisement no., post, department) and Personal Details (name, DOB, contact, address, photo upload, ID proof upload). Data is saved to `applicationdetails` and `personaldetails` tables.
    *   **Page 2 (`/formpages/2`):** Educational Qualifications (PhD, PG, UG, Schooling). Data is saved to `educationaldetails` and `edu_additionaldetails` tables.
    *   **Page 3 (`/formpages/3`):** Employment Details (Present Employment, Employment History, Teaching Experience, Research Experience, Industrial Experience) and Areas of Specialization/Research. Data is saved to `presentemployment`, `employmenthistory`, `teachingexp`, `researchexp`, `industrialexp`, and `aos_aor` tables.
    *   **Page 4 (`/formpages/4`):** Publication Summary, Best 10 Publications, Patents, Books, Book Chapters, and Google Scholar Link. Data is saved to `publications`, `top10publications`, `patents`, `books`, `book_chapters`, and `googlelink` tables.
    *   **Page 5 (`/formpages/5`):** Professional Details (Memberships, Trainings, Awards) and Sponsored Projects/Consultancy. Data is saved to `membership`, `training`, `awards`, `sponsoredprojects`, and `consultancyprojects` tables.
    *   **Page 6 (`/formpages/6`):** Thesis Supervision (PhD, PG, UG). Data is saved to `phd_thesis`, `pg_thesis`, and `ug_thesis` tables.
    *   **Page 7 (`/formpages/7`):** Statements (Research, Teaching), Relevant Info, Professional Service, Journal/Conference Details. Data is saved to the `page_7` table.
    *   **Page 8 (`/formpages/8`):** Uploads (Certificates for PhD, PG, UG, 10th, 12th, Payslip, NOC, Post-PhD experience, Misc, Best Paper, Signature) and Referees. Uploaded file paths are saved to `page_8_upload`, and referee details are saved to `datapage`.
    *   **Page 9 (`/formpages/9`):** Declaration and Final Submission. This page presents a final checklist and allows the user to formally submit their application.
    *   Throughout these form pages, data is typically deleted and re-inserted for the user's email on each POST request to ensure the latest information is saved. Previously saved data for the logged-in user is fetched from the database and pre-filled in the forms when a page is loaded.

5.  **Final Application Preview/Print (`/printform`):**
    *   After completing all form pages (or perhaps after the final submission on Page 9), users can access this page.
    *   It fetches all the data submitted by the user from the various database tables.
    *   The data is then rendered into a comprehensive view, suitable for printing or saving as a PDF.

6.  **Logout (`/logout`):**
    *   Users can log out of the application.
    *   The session is destroyed, and the user is typically redirected to the login page.

This flow ensures a systematic collection of all necessary information for the faculty recruitment process. The use of `isAuthenticated` middleware protects routes that require a logged-in user.

## API Endpoints / Routes

The application defines several routes to handle user authentication, navigation, form submissions, and other actions. All routes are prefixed by the base URL (e.g., `http://localhost:8000`). The `isAuthenticated` middleware is used to protect routes that require users to be logged in.

### Authentication Routes

*   **`GET /signup`**: Displays the user registration page.
*   **`POST /signup`**: Handles user registration. Collects form data, validates, hashes password, saves user to `users` and `profile` tables. Redirects to `/login`.
*   **`GET /login`**: Displays the login page.
*   **`POST /login`**: Handles user login using Passport.js (`local` strategy). Redirects to `/formpages/1` on success, or back to `/login` on failure.
*   **`GET /logout`**: Logs the user out by destroying the session. Redirects to `/login`.
*   **`GET /reset`**: Displays the page for users to enter their email to initiate password reset.
*   **`POST /reset`**: Handles the initiation of password reset. Sends a reset link with a token to the user's email.
*   **`GET /reset-password/:token`**: Displays the form for users to enter a new password, using the token from the email link.
*   **`POST /reset-password/:token`**: Handles the submission of the new password. Updates the password in the `users` table.

### Application Form Routes (`/formpages/*`)

These routes handle the multi-page application form. Each page typically has a GET route to display the form (often pre-filling data from the session or database) and a POST route to process the submitted data. User must be authenticated to access these.

*   **`GET /formpages/1`**: Displays Page 1 of the application form (Application & Personal Details).
*   **`POST /formpages/1`**: Submits data for Page 1. Handles file uploads for user photo and ID proof. Saves data to `applicationdetails` and `personaldetails`. Redirects to `/formpages/2`.
*   **`GET /formpages/2`**: Displays Page 2 (Educational Qualifications).
*   **`POST /formpages/2`**: Submits data for Page 2. Saves data to `educationaldetails` and `edu_additionaldetails`. Redirects to `/formpages/3`.
*   **`GET /formpages/3`**: Displays Page 3 (Employment Details, Areas of Specialization/Research).
*   **`POST /formpages/3`**: Submits data for Page 3. Saves data to `presentemployment`, `employmenthistory`, `teachingexp`, `researchexp`, `industrialexp`, `aos_aor`. Redirects to `/formpages/4`.
*   **`GET /formpages/4`**: Displays Page 4 (Publications, Patents, Books, Google Scholar Link).
*   **`POST /formpages/4`**: Submits data for Page 4. Saves data to `publications`, `top10publications`, `patents`, `books`, `book_chapters`, `googlelink`. Redirects to `/formpages/5`.
*   **`GET /formpages/5`**: Displays Page 5 (Professional Details, Sponsored Projects/Consultancy).
*   **`POST /formpages/5`**: Submits data for Page 5. Saves data to `membership`, `training`, `awards`, `sponsoredprojects`, `consultancyprojects`. Redirects to `/formpages/6`.
*   **`GET /formpages/6`**: Displays Page 6 (Thesis Supervision).
*   **`POST /formpages/6`**: Submits data for Page 6. Saves data to `phd_thesis`, `pg_thesis`, `ug_thesis`. Redirects to `/formpages/7`.
*   **`GET /formpages/7`**: Displays Page 7 (Statements, Relevant Info, etc.).
*   **`POST /formpages/7`**: Submits data for Page 7. Saves data to `page_7`. Redirects to `/formpages/8`.
*   **`GET /formpages/8`**: Displays Page 8 (Uploads and Referees).
*   **`POST /formpages/8`**: Submits data for Page 8. Handles multiple file uploads (certificates, signature, etc.). Saves file paths to `page_8_upload` and referee details to `datapage`. Redirects to `/formpages/9`.
*   **`GET /formpages/9`**: Displays Page 9 (Declaration and Final Submission).
*   **`POST /formpages/9`**: Handles the final submission process. Redirects to `/printform`.

### Final Print/Preview Route

*   **`GET /printform`**: Displays a consolidated view of the entire application submitted by the user, suitable for printing. Fetches data from all relevant tables for the logged-in user. User must be authenticated.

### Miscellaneous

*   **`GET /`**: Redirects to `/login`.

This route structure supports the comprehensive data collection and user management features of the recruitment portal. File uploads are handled by `multer` and paths (often Cloudinary URLs) are stored in the database.
