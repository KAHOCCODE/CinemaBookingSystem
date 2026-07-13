# Cinema Booking System

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4)](https://dotnet.microsoft.com/)
[![ASP.NET Core MVC](https://img.shields.io/badge/ASP.NET%20Core-MVC-512BD4)](https://learn.microsoft.com/aspnet/core/mvc/)
[![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-CC2927)](https://www.microsoft.com/sql-server)
[![Build](https://github.com/KAHOCCODE/CinemaBookingSystem/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/KAHOCCODE/CinemaBookingSystem/actions/workflows/ci.yml)

Cinema Booking System is a web application for cinema management and online movie ticket booking. The system provides features for customers, employees, and administrators, including movie management, showtime scheduling, seat selection, ticket booking, food ordering, promotions, refunds, reviews, loyalty points, and revenue reporting.

The repository can be used for learning, development, testing, and further improvement of an ASP.NET Core MVC cinema booking application.

---

## Table of Contents

- [Overview](#overview)
- [Technologies](#technologies)
- [Main Features](#main-features)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Database Setup](#database-setup)
- [Application Configuration](#application-configuration)
- [Running the Application](#running-the-application)
- [Continuous Integration](#continuous-integration)
- [Security Notes](#security-notes)
- [Development Notes](#development-notes)
- [Roadmap](#roadmap)
- [Team](#team)
- [Contributing](#contributing)
- [Project Status](#project-status)
- [Disclaimer](#disclaimer)

---

## Overview

The application supports the core operations of a cinema booking platform:

- Customers can browse movies and available showtimes.
- Customers can select seats and book movie tickets.
- Customers can order food and drinks together with their tickets.
- Customers can review movies and manage booking history.
- Employees can manage movies, schedules, tickets, orders, customers, and promotions.
- Administrators can monitor cinema operations and revenue reports.

The application follows the ASP.NET Core MVC pattern and uses Entity Framework Core to communicate with Microsoft SQL Server.

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
- Entity Framework Core Migrations

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
- Visual Studio 2022
- Git and GitHub
- GitHub Actions

---

## Main Features

### Customer Features

- Register, sign in, and sign out
- Update personal information
- Browse currently showing and upcoming movies
- Search for movies
- View movie details and available showtimes
- Select one or more seats
- Order food and drinks
- Apply available promotions
- Confirm ticket bookings
- View booking history and ticket information
- Cancel eligible tickets
- Submit refund requests
- Review and rate movies
- Earn and use loyalty points
- Receive account-related email notifications

### Employee and Administration Features

- Employee authentication
- Administration dashboard
- Movie and movie genre management
- Showtime management
- Screening room and seat management
- Customer management
- Employee and position management
- Ticket and order management
- Food and beverage management
- Promotion management
- Refund request management
- Movie review management
- Revenue statistics
- Excel report export

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
│   │       └── Views/
│   ├── Controllers/
│   ├── Migrations/
│   ├── Models/
│   ├── Properties/
│   ├── ViewModels/
│   ├── Views/
│   ├── wwwroot/
│   ├── Program.cs
│   ├── appsettings.json
│   └── CinemaBookingSystem.csproj
│
├── CinemaBookingSystem.sln
├── .gitignore
└── README.md
```

---

## Getting Started

### Prerequisites

Install the following tools:

- [Visual Studio 2022](https://visualstudio.microsoft.com/)
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Microsoft SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads)
- [SQL Server Management Studio](https://learn.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
- [Git](https://git-scm.com/)

Check the installed .NET version:

```bash
dotnet --version
```

The result should be version `8.x`.

### Clone the Repository

```bash
git clone https://github.com/KAHOCCODE/CinemaBookingSystem.git
cd CinemaBookingSystem
```

Restore NuGet packages:

```bash
dotnet restore CinemaBookingSystem.sln
```

Build the solution:

```bash
dotnet build CinemaBookingSystem.sln
```

---

## Database Setup

The SQL Server database resources for this project are stored in the following shared Google Drive folder:

### [Download Database Scripts](https://drive.google.com/drive/folders/1y_l4osMHSJ8BLCZSf9YY_NyhupAmsfQW?usp=sharing)

The recommended setup method is to download and execute the provided SQL Server script.

### Import a `.sql` Script

1. Open SQL Server Management Studio.
2. Connect to a local SQL Server instance.
3. Open the downloaded `.sql` file.
4. Review the database name defined in the script.
5. Execute the script.
6. Refresh the **Databases** folder.
7. Verify that the required tables and sample data were created.

When the script does not create a database automatically, create one first:

```sql
CREATE DATABASE QLRapPhim;
GO

USE QLRapPhim;
GO
```

Then execute the remaining script content against that database.

### Restore a `.bak` Backup

When a `.bak` backup is available:

1. Open SQL Server Management Studio.
2. Right-click **Databases**.
3. Select **Restore Database**.
4. Choose **Device**.
5. Add the downloaded `.bak` file.
6. Select the backup set.
7. Confirm the destination database name.
8. Select **OK** to restore the database.

### Entity Framework Core Migrations

The repository contains incremental Entity Framework Core migrations created during development. These migrations may require the baseline database schema to exist before they are applied.

After importing the baseline database, apply pending migrations when necessary:

```bash
dotnet tool install --global dotnet-ef
dotnet ef database update --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Use one primary database setup method to avoid duplicate or conflicting database structures.

---

## Application Configuration

The application reads the SQL Server connection string using the key:

```text
ConnectionStrings:QLRapPhim
```

For local development, store sensitive values with .NET User Secrets instead of committing them to GitHub.

Initialize User Secrets:

```bash
dotnet user-secrets init --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Set the local SQL Server connection string:

```bash
dotnet user-secrets set "ConnectionStrings:QLRapPhim" "Server=YOUR_SERVER;Database=QLRapPhim;Trusted_Connection=True;TrustServerCertificate=True" --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Example for SQL Server Express:

```bash
dotnet user-secrets set "ConnectionStrings:QLRapPhim" "Server=.\SQLEXPRESS;Database=QLRapPhim;Trusted_Connection=True;TrustServerCertificate=True" --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Example for LocalDB:

```bash
dotnet user-secrets set "ConnectionStrings:QLRapPhim" "Server=(localdb)\MSSQLLocalDB;Database=QLRapPhim;Trusted_Connection=True;TrustServerCertificate=True" --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

### SMTP Configuration

The application may require SMTP configuration for account-related email features.

```bash
dotnet user-secrets set "SmtpSettings:Host" "smtp.gmail.com" --project CinemaBookingSystem/CinemaBookingSystem.csproj
dotnet user-secrets set "SmtpSettings:Port" "587" --project CinemaBookingSystem/CinemaBookingSystem.csproj
dotnet user-secrets set "SmtpSettings:Username" "YOUR_EMAIL" --project CinemaBookingSystem/CinemaBookingSystem.csproj
dotnet user-secrets set "SmtpSettings:Password" "YOUR_APP_PASSWORD" --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Use an application password when supported by the email provider.

---

## Running the Application

Run the project from the command line:

```bash
dotnet run --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Alternatively:

1. Open `CinemaBookingSystem.sln` in Visual Studio 2022.
2. Set `CinemaBookingSystem` as the startup project.
3. Select the HTTPS launch profile.
4. Run the application.

The local address is displayed in the Visual Studio output window or terminal. The actual port depends on `Properties/launchSettings.json`.

---

## Continuous Integration

The repository uses GitHub Actions for automatic build validation.

The workflow:

1. Checks out the repository.
2. Installs the required .NET SDK.
3. Restores NuGet dependencies.
4. Builds the solution in Release configuration.

Workflow file:

```text
.github/workflows/ci.yml
```

Cloud deployment is not currently configured. The repository currently focuses on reliable build validation.

---

## Security Notes

Do not commit sensitive information such as:

- Database passwords
- SMTP passwords
- API keys
- Access tokens
- Azure publish profiles
- Production connection strings
- Private credentials

Recommended configuration methods:

- .NET User Secrets for local development
- Environment variables
- GitHub Actions Secrets
- Secret managers provided by the deployment platform

Any credential accidentally committed to source control should be revoked and replaced.

---

## Development Notes

The project is being improved gradually to increase maintainability, security, and clarity.

Current technical considerations include:

- Some namespaces and identifiers may still use legacy project names.
- Existing migrations are incremental and may require a baseline database.
- Some controllers contain multiple responsibilities and can be separated into services.
- The booking workflow requires additional transaction and concurrency protection.
- Automated tests are still limited.

These points do not prevent local study or development, but they should be considered when extending the application.

---

## Roadmap

### Security

- Remove remaining hard-coded credentials
- Protect the Admin area with role-based authorization
- Add anti-forgery validation to form submissions
- Use secure password reset tokens
- Validate uploaded files

### Architecture

- Rename remaining legacy namespaces
- Refactor large controllers
- Introduce a service layer
- Use dedicated ViewModels
- Reduce direct database access from controllers
- Separate booking, email, file, and reporting services

### Booking Process

- Use database transactions when creating bookings
- Prevent duplicate seat reservations
- Improve ticket and order relationships
- Prevent duplicate bookings caused by page refresh
- Improve cancellation and refund rules

### Testing

- Add unit tests for booking calculations
- Add tests for seat availability
- Add tests for promotions and refunds
- Add integration tests for authentication and booking workflows

### Documentation

- Add application screenshots
- Add an entity relationship diagram
- Add demo account instructions
- Add booking flow documentation

---

## Team

This project was originally developed by a four-member university team:

- Nguyễn Hòa Khang
- Phan Nguyễn Đăng Khoa
- Trương Minh Đức
- Đỗ Hoàng Ka

The repository has since been maintained and improved through additional refactoring, documentation, and configuration updates.

---

## Contributing

Contributions are welcome.

Recommended workflow:

1. Fork or clone the repository.
2. Create a feature branch.
3. Make focused changes.
4. Build and test the project locally.
5. Commit with a clear message.
6. Open a pull request describing the change.

Example:

```bash
git switch -c feature/improve-seat-selection
git add .
git commit -m "feat: improve seat selection validation"
git push -u origin feature/improve-seat-selection
```

Please avoid committing credentials, generated build folders, or machine-specific configuration.

---

## Project Status

```text
Status: Active Development and Refactoring
Framework: ASP.NET Core MVC
Runtime: .NET 8
Database: Microsoft SQL Server
CI: GitHub Actions Build Validation
Deployment: Local Development
```

The application is functional and can be used as a foundation for learning, testing, and further development.

---

## Disclaimer

This project was created for educational and development purposes.

Additional security review, testing, monitoring, and deployment configuration are required before production use.
