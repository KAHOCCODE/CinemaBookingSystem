# Cinema Booking System

Cinema Booking System is a web application for cinema management and online movie ticket booking. The system provides separate features for customers and cinema employees, including movie management, showtime scheduling, seat selection, food ordering, ticket booking, promotions, refunds, reviews, and revenue reporting.

This project was originally developed as a university team project and is currently being refactored and documented for an Intern/Fresher .NET Developer portfolio.

---

## Table of Contents

- [Overview](#overview)
- [Technologies](#technologies)
- [Main Features](#main-features)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Database Configuration](#database-configuration)
- [Connection String](#connection-string)
- [Email Configuration](#email-configuration)
- [Running the Application](#running-the-application)
- [Continuous Integration](#continuous-integration)
- [Security Notes](#security-notes)
- [Team Project](#team-project)
- [My Current Contributions](#my-current-contributions)
- [Improvement Roadmap](#improvement-roadmap)
- [Project Status](#project-status)
- [Disclaimer](#disclaimer)

---

## Overview

The application supports the main operations of a cinema ticket booking system:

- Customers can browse movies and showtimes.
- Customers can select seats and book movie tickets.
- Customers can order food and drinks together with their tickets.
- Customers can review movies and manage their booking history.
- Employees can manage movies, schedules, tickets, orders, customers, and promotions.
- Administrators can monitor cinema operations and revenue reports.

The project follows the ASP.NET Core MVC pattern and uses Entity Framework Core to communicate with SQL Server.

---

## Technologies

### Backend

- C#
- .NET 8
- ASP.NET Core MVC
- Entity Framework Core
- LINQ
- Cookie Authentication
- BCrypt.Net

### Database

- Microsoft SQL Server
- SQL Server Management Studio
- Entity Framework Core

### Frontend

- Razor Views
- HTML5
- CSS3
- JavaScript
- Bootstrap
- jQuery

### Libraries and Tools

- EPPlus for Excel report generation
- ZXing.Net for QR code and barcode generation
- Git
- GitHub
- GitHub Actions
- Visual Studio 2022

---

## Main Features

### Customer Features

- Register a customer account
- Sign in and sign out
- Update personal information
- Browse currently showing movies
- Browse upcoming movies
- Search for movies
- View movie details
- View movie genres
- View available showtimes
- Select a screening room
- Select one or more seats
- Order food and drinks
- Apply available promotions
- Confirm ticket booking
- View booking history
- View ticket information
- Cancel eligible tickets
- Submit refund requests
- Review and rate movies
- Earn and use loyalty points
- Receive account-related email notifications

### Employee and Administration Features

- Employee authentication
- Administration dashboard
- Movie management
- Movie genre management
- Showtime management
- Screening room management
- Seat management
- Customer management
- Employee management
- Employee position management
- Ticket management
- Order management
- Food and beverage management
- Promotion management
- Refund request management
- Movie review management
- Revenue statistics
- Report export to Excel

---

## Project Structure

```text
CinemaBookingSystem/
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── CinemaBookingSystem/
│   ├── Areas/
│   │   └── Admin/
│   │       ├── Controllers/
│   │       ├── Models/
│   │       └── Views/
│   │
│   ├── Controllers/
│   ├── Models/
│   ├── ViewModels/
│   ├── Views/
│   ├── wwwroot/
│   ├── Properties/
│   ├── Program.cs
│   ├── appsettings.json
│   └── CinemaBookingSystem.csproj
│
├── CinemaBookingSystem.sln
├── .gitignore
└── README.md
```

The current project is being gradually refactored to improve separation of concerns between controllers, services, view models, and database access.

---

## Getting Started

### Prerequisites

Install the following tools before running the project:

- Visual Studio 2022
- .NET 8 SDK
- Microsoft SQL Server
- SQL Server Management Studio
- Git

Check the installed .NET version:

```bash
dotnet --version
```

The result should be version `8.x` or later.

---

## Clone the Repository

```bash
git clone https://github.com/KAHOCCODE/CinemaBookingSystem.git
cd CinemaBookingSystem
```

Restore the NuGet packages:

```bash
dotnet restore CinemaBookingSystem.sln
```

Build the solution:

```bash
dotnet build CinemaBookingSystem.sln
```

---

## Database Configuration

### Create the Database

Create a SQL Server database for the application.

Example database name:

```text
CinemaBookingSystem
```

Depending on the current database setup, use one of the following methods.

### Option 1: Entity Framework Core Migrations

If the project contains Entity Framework Core migrations, run:

```bash
dotnet ef database update --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Install the Entity Framework command-line tool when necessary:

```bash
dotnet tool install --global dotnet-ef
```

### Option 2: SQL Script

If the repository contains a database script:

1. Open SQL Server Management Studio.
2. Connect to the local SQL Server instance.
3. Create or select the target database.
4. Open the provided `.sql` file.
5. Execute the script.
6. Verify that all required tables have been created.

---

## Connection String

Do not commit real database credentials to the repository.

For local development, use .NET User Secrets or environment variables.

Initialize User Secrets:

```bash
dotnet user-secrets init --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Add the database connection string:

```bash
dotnet user-secrets set "ConnectionStrings:YourConnectionStringName" "Server=YOUR_SERVER;Database=CinemaBookingSystem;Trusted_Connection=True;TrustServerCertificate=True" --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Replace `YourConnectionStringName` with the connection string key currently used in `Program.cs`.

Example connection string using Windows Authentication:

```text
Server=localhost;Database=CinemaBookingSystem;Trusted_Connection=True;TrustServerCertificate=True
```

Example connection string using SQL Server Authentication:

```text
Server=localhost;Database=CinemaBookingSystem;User Id=YOUR_USERNAME;Password=YOUR_PASSWORD;TrustServerCertificate=True
```

Never commit real usernames, passwords, email credentials, access tokens, API keys, or Azure publish profiles.

---

## Email Configuration

The application may require SMTP configuration for account-related email features.

Sensitive SMTP information should be stored using User Secrets:

```bash
dotnet user-secrets set "SmtpSettings:Host" "smtp.gmail.com" --project CinemaBookingSystem/CinemaBookingSystem.csproj

dotnet user-secrets set "SmtpSettings:Port" "587" --project CinemaBookingSystem/CinemaBookingSystem.csproj

dotnet user-secrets set "SmtpSettings:Username" "YOUR_EMAIL" --project CinemaBookingSystem/CinemaBookingSystem.csproj

dotnet user-secrets set "SmtpSettings:Password" "YOUR_APP_PASSWORD" --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Use an application password instead of a normal email account password when the email provider supports it.

---

## Running the Application

Run the project from the command line:

```bash
dotnet run --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Alternatively, open `CinemaBookingSystem.sln` in Visual Studio 2022 and run the application using HTTPS.

The local address is displayed in the Visual Studio output window or terminal.

Typical development addresses may look like:

```text
https://localhost:7000
http://localhost:5000
```

The actual port depends on the current `launchSettings.json` configuration.

---

## Continuous Integration

The repository uses GitHub Actions to validate the project automatically.

The workflow performs the following steps:

1. Checks out the repository.
2. Installs the required .NET SDK.
3. Restores NuGet dependencies.
4. Builds the solution in Release configuration.

The workflow runs when:

- New code is pushed to the configured branch.
- A pull request is created.
- The workflow is started manually.

Workflow file:

```text
.github/workflows/ci.yml
```

Cloud deployment is not currently configured. The previous Azure App Service subscription is no longer active, so the repository currently focuses on reliable build validation.

---

## Security Notes

The following information must not be committed to GitHub:

- Database passwords
- SMTP passwords
- Azure publish profiles
- API keys
- Access tokens
- Private connection strings
- Production credentials
- Personal secrets

Recommended configuration methods:

- .NET User Secrets for local development
- Environment variables
- GitHub Actions Secrets
- Azure Key Vault for production environments

Sensitive values that were previously exposed should be revoked and replaced.

---

## Team Project

This project was originally developed as a four-member university project.

### Team Members

- Nguyễn Hòa Khang
- Phan Nguyễn Đăng Khoa
- Trương Minh Đức
- Đỗ Hoàng Ka

Each member was responsible for different parts of the system during the original development phase.

---

## My Current Contributions

Current repository maintenance and portfolio preparation by Đỗ Hoàng Ka include:

- Renamed the repository to `CinemaBookingSystem`
- Renamed the solution and project files
- Updated the project structure and naming
- Replaced the obsolete Azure deployment workflow
- Added GitHub Actions build validation
- Updated deprecated GitHub Actions dependencies
- Removed inactive Azure deployment configuration
- Removed obsolete Azure repository secrets
- Improved repository documentation
- Reviewed configuration and security issues
- Prepared the repository for an Intern/Fresher .NET Developer portfolio

The original feature contributions should be described here based only on the modules personally implemented during the team project.

Examples that may be added after verification:

```text
- Developed movie and showtime management
- Implemented food and order management
- Built the movie review module
- Implemented ticket cancellation and refund processing
- Designed administration pages
- Created SQL Server tables and relationships
```

Only include responsibilities that can be explained clearly during a technical interview.

---

## Improvement Roadmap

The project is currently being improved in stages.

### Security

- Remove hard-coded connection strings
- Remove hard-coded email credentials
- Protect the Admin area with authorization
- Improve role-based access control
- Add anti-forgery validation to form submissions
- Improve password reset using secure tokens
- Validate uploaded files

### Architecture

- Refactor large controllers
- Introduce a service layer
- Introduce dedicated ViewModels
- Reduce direct database access from controllers
- Improve dependency injection
- Separate file, email, booking, and reporting services
- Improve naming consistency

### Booking Process

- Use database transactions when creating bookings
- Prevent duplicate seat reservations
- Replace comma-separated seat storage
- Improve ticket and order relationships
- Prevent duplicate bookings caused by page refresh
- Improve booking confirmation
- Improve ticket cancellation and refund rules

### Database

- Improve entity relationships
- Replace unsafe manual identifier generation
- Add unique indexes
- Improve password column length
- Add database migrations
- Improve seed data
- Improve status management using constants or enums

### Testing

- Add unit tests for booking calculations
- Add tests for seat availability
- Add tests for promotions
- Add tests for refund conditions
- Add integration tests for authentication
- Add integration tests for booking workflows

### User Interface

- Improve responsive layout
- Improve the administration dashboard
- Add clearer validation messages
- Add toast notifications
- Improve seat selection
- Improve mobile compatibility
- Improve accessibility

### Documentation

- Add application screenshots
- Add an entity relationship diagram
- Add booking flow documentation
- Add database setup instructions
- Add demo account instructions
- Add architecture documentation

---

## Project Status

```text
Status: Active Refactoring
Purpose: Intern/Fresher .NET Developer Portfolio
Framework: ASP.NET Core MVC
Runtime: .NET 8
Database: SQL Server
CI Status: GitHub Actions Build Validation
Deployment: Local Development
```

The project is functional but is still being improved in security, architecture, documentation, testing, and maintainability.

---

## Disclaimer

This project was created for educational and portfolio purposes.

It is not currently intended for production use without additional security review, testing, database migration planning, monitoring, and deployment configuration.
