# Census Management System

A desktop application for digitizing population census data collection, household management, and demographic analysis — built for Pakistan's census operations and styled after NADRA's official green/white government theme.

![.NET](https://img.shields.io/badge/.NET-10.0-512BD4?logo=dotnet)
![WPF](https://img.shields.io/badge/WPF-Desktop-0078D4)
![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-CC2927?logo=microsoftsqlserver)
![License](https://img.shields.io/badge/license-MIT-green)

---

## Overview

The Census Management System replaces manual, paper-based census data collection with a fully digital desktop workflow. Enumerators can register households and record person-level demographic data in real time, while administrators monitor progress, manage geographic hierarchy, and generate analytical reports — all through a modern, government-style interface.

## Features

- **Role-based authentication** — Admin and Enumerator roles with SHA-256 salted password hashing
- **Dashboard** — Real-time KPI cards (total households, population, literacy rate, gender split, pending surveys) and recent activity feed
- **Household management** — Full CRUD with cascading Province → District → Union Council selection, search, and status filtering
- **Person / population records** — CNIC, demographics, education, occupation, and household relationship tracking
- **Geographic hierarchy** — Manage Provinces, Districts, and Union Councils (pre-seeded with 7 provinces, 19 districts, 17 UCs)
- **Reports & analytics** — Interactive charts (population, gender, age groups, housing, income) with Excel and PDF export
- **User management** — Admin-only console for creating/editing/deactivating system accounts
- **Settings** — Configurable database connection, Windows/SQL authentication toggle, password change

## Tech Stack

| Layer | Technology |
|---|---|
| UI Framework | WPF (.NET 10.0) |
| UI Library | MahApps.Metro 2.4.10 + IconPacks 4.11.0 |
| Database | Microsoft SQL Server |
| Data Access | Microsoft.Data.SqlClient 5.2.0 |
| Charts | SkiaSharp / LiveCharts |
| Excel Export | ClosedXML 0.102.2 |
| PDF Export | iText7 8.0.4 |

## Project Structure

```
AP_Project/
├── Database/
│   └── CensusDB_CreateScript.sql     # Full schema + seed data
├── Helpers/
│   └── DatabaseHelper.cs              # Connection & query execution
├── Models/
│   └── Models.cs                      # POCO entities
├── Services/
│   ├── AuthService.cs                 # Login, sessions, password change
│   ├── HouseholdService.cs
│   ├── PersonService.cs
│   ├── LocationService.cs
│   └── UserService.cs
├── Views/
│   ├── LoginWindow.xaml
│   ├── ShellWindow.xaml                # Main app shell + sidebar nav
│   ├── DashboardPage.xaml
│   ├── HouseholdsPage.xaml
│   ├── HouseholdFormWindow.xaml
│   ├── HouseholdMembersWindow.xaml
│   ├── PersonsPage.xaml
│   ├── PersonFormWindow.xaml
│   ├── LocationsPage.xaml
│   ├── ReportsPage.xaml
│   ├── UsersPage.xaml
│   └── SettingsPage.xaml
├── Resources/
│   └── AppStyles.xaml                  # Theme tokens & control styles
└── AP_Project.csproj
```

## Getting Started

### Prerequisites

- Windows 10/11 (64-bit)
- [.NET 10.0 Desktop Runtime](https://dotnet.microsoft.com/download)
- Visual Studio 2022 with the **.NET Desktop Development** workload
- Microsoft SQL Server (Express or higher) + SQL Server Management Studio

### Database Setup

1. Open SQL Server Management Studio and connect to your instance
2. Open `AP_Project/Database/CensusDB_CreateScript.sql`
3. Press **F5** to execute — confirm you see `Database Setup Complete!`

### Run the App

```bash
git clone https://github.com/<your-username>/census-management-system.git
cd census-management-system/AP_Project
dotnet restore
dotnet build
```

Update the connection string server name in `Views/LoginWindow.xaml.cs` if your SQL Server instance isn't `localhost`, then:

```bash
dotnet run
```

Or open `AP_Project.sln` in Visual Studio and press **F5**.

### Default Login Credentials

| Role | Username | Password |
|---|---|---|
| Admin | `admin` | `admin123` |
| Enumerator | `enumerator1` | `enum123` |

## Database Schema

7 normalized tables with enforced foreign key integrity:

`Users` → `Provinces` → `Districts` → `UnionCouncils` → `Households` → `Persons`

All seed data uses name-based `JOIN` lookups instead of hardcoded IDENTITY values, so the script runs cleanly regardless of database state.

## Screenshots

<img width="424" height="265" alt="image" src="https://github.com/user-attachments/assets/c54f6076-b52e-42a1-b5a2-cca4c7eaa085" />
<img width="599" height="308" alt="image" src="https://github.com/user-attachments/assets/08f1484a-5ada-443e-b8d0-e9d3f75b3488" />
<img width="599" height="311" alt="image" src="https://github.com/user-attachments/assets/e8618bd2-d5d4-4ea0-a565-a5292d8377f4" />



## License

This project is licensed under the MIT License.

## Author

**Muhammad Kumail Abbas**
F23605093 — CS Department, National University of Technology (NUTECH)
