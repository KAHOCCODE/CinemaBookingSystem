# Cinema Booking System

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4)](https://dotnet.microsoft.com/)
[![ASP.NET Core MVC](https://img.shields.io/badge/ASP.NET%20Core-MVC-512BD4)](https://learn.microsoft.com/aspnet/core/mvc/)
[![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-CC2927)](https://www.microsoft.com/sql-server)
[![Build](https://github.com/KAHOCCODE/CinemaBookingSystem/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/KAHOCCODE/CinemaBookingSystem/actions/workflows/ci.yml)

Cinema Booking System is a web application for cinema management and online movie ticket booking. It provides separate features for customers and cinema employees, including movie management, showtime scheduling, seat selection, ticket booking, food ordering, promotions, refunds, reviews, loyalty points, and revenue reporting.

This project was originally developed as a university team project and is currently being refactored and documented for an Intern/Fresher .NET Developer portfolio.

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
- [Team Project](#team-project)
- [My Current Contributions](#my-current-contributions)
- [Improvement Roadmap](#improvement-roadmap)
- [Project Status](#project-status)

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

### [Download Database Files](https://drive.google.com/drive/folders/1y_l4osMHSJ8BLCZSf9YY_NyhupAmsfQW?usp=sharing)

Download the available database file and use the instructions that match its file type.

### Option 1: Import a `.sql` Script

1. Open SQL Server Management Studio.
2. Connect to your local SQL Server instance.
3. Open the downloaded `.sql` file.
4. Review the database name defined in the script.
5. Execute the script.
6. Refresh the **Databases** folder and verify that the required tables were created.

When the script does not create a database automatically, create one first:

```sql
CREATE DATABASE QLRapPhim;
GO

USE QLRapPhim;
GO
```

Then execute the remaining script content against that database.

### Option 2: Restore a `.bak` Backup

1. Open SQL Server Management Studio.
2. Right-click **Databases**.
3. Select **Restore Database**.
4. Choose **Device**.
5. Add the downloaded `.bak` file.
6. Select the backup set.
7. Confirm the destination database name.
8. Select **OK** to restore the database.

### Option 3: Apply Entity Framework Core Migrations

The repository also contains an Entity Framework Core `Migrations` folder. To apply the existing migrations, configure the connection string first and run:

```bash
dotnet tool install --global dotnet-ef
dotnet ef database update --project CinemaBookingSystem/CinemaBookingSystem.csproj
```

Use only one primary setup method to avoid creating duplicate or conflicting database structures.

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

Do not commit real database passwords, SMTP passwords, API keys, access tokens, Azure publish profiles, or production credentials.

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

## Team Project

This project was originally developed by a four-member university team.

### Team Members

- Nguyễn Hòa Khang
- Phan Nguyễn Đăng Khoa
- Trương Minh Đức
- Đỗ Hoàng Ka

Each member was responsible for different parts of the original system.

---

## My Current Contributions

Current repository maintenance and portfolio preparation by **Đỗ Hoàng Ka** include:

- Renamed the repository to `CinemaBookingSystem`
- Renamed the solution and project files
- Updated project naming and repository structure
- Replaced the obsolete Azure deployment workflow
- Added GitHub Actions build validation
- Updated deprecated GitHub Actions dependencies
- Removed inactive Azure deployment configuration
- Removed obsolete Azure repository secrets
- Improved repository documentation
- Added database download and setup instructions
- Reviewed configuration and security issues
- Prepared the repository for an Intern/Fresher .NET Developer portfolio

Original feature contributions should only be added after verifying the modules personally implemented during the team project.

---

## Improvement Roadmap

### Security

- Remove remaining hard-coded connection strings and email credentials
- Protect the Admin area with role-based authorization
- Add anti-forgery validation to form submissions
- Replace password reset by email password delivery with secure reset tokens
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

## Project Status

```text
Status: Active Refactoring
Purpose: Intern/Fresher .NET Developer Portfolio
Framework: ASP.NET Core MVC
Runtime: .NET 8
Database: Microsoft SQL Server
CI: GitHub Actions Build Validation
Deployment: Local Development
```

The project is functional but is still being improved in security, architecture, testing, and maintainability.

---

## Disclaimer

This project was created for educational and portfolio purposes.

It is not intended for production use without additional security review, testing, monitoring, and deployment configuration.
