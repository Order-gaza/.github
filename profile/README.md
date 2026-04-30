# Order - Comprehensive Delivery & E-Commerce Platform

<div align="center">

![Order Platform Logo](https://github.com/Order-gaza/.github/blob/main/launcher1.jpg)

**Streamlining Logistics and E-Commerce Operations Through Advanced Technology**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Flutter](https://img.shields.io/badge/Flutter-3.6+-02569B?logo=flutter)](https://flutter.dev)
[![PHP](https://img.shields.io/badge/PHP-8.0+-777BB4?logo=php)](https://php.net)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Google Play](https://img.shields.io/badge/Google_Play-Download-34A853?logo=google-play&logoColor=white)](https://play.google.com/store/apps/details?id=com.yasser.order)

[Features](#features) • [Architecture](#architecture) • [Getting Started](#getting-started) • [Documentation](#documentation) • [Contributing](#contributing)

</div>

---

## 🎯 About

**Order** is a comprehensive, multi-platform e-commerce and delivery management ecosystem. Built with modern, scalable technologies, this platform bridges the gap between customers, regional vendors, and logistics administrators, ensuring a seamless, real-time order fulfillment pipeline.

### 📲 Download the Customer App

<a href="https://play.google.com/store/apps/details?id=com.yasser.order">
  <img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" alt="Get it on Google Play" height="80">
</a>

### Platform Components

Our platform consists of three tightly integrated repositories:

| Component | Technology | Purpose | Repository |
|-----------|-----------|---------|------------|
| **Customer App** | Flutter / GetX | Mobile shopping and order tracking | [order_app](./order_app) · [▶ Play Store](https://play.google.com/store/apps/details?id=com.yasser.order) |
| **Admin Panel** | Flutter / GetX | System administration and vendor operations | [order_admin](./order_admin) |
| **Backend API** | PHP / MySQL | Secure RESTful API and core business logic | [backend](./backend) |

---

## ✨ Key Highlights

### 🛍️ Customer Experience
- **Dynamic Catalog**: Browse through vendor items with smooth image caching and dynamic UI states.
- **Intelligent Cart System**: Cart validation strictly checks for regional coverage and real-time vendor availability before checkout.
- **Order Tracking**: End-to-end real-time visibility from pending to delivered status.
- **Push Notifications**: Instant alerts via Firebase Cloud Messaging for critical order updates.
- **Favorites & Profile Management**: Persistent user preferences and secure tokenized sessions.

### 👨‍💼 Business & Vendor Management
- **Order Pipeline Control**: Strict state machine enforcement (Admin Confirm → Vendor Accept).
- **Vendor Status Overrides**: Automated business hours toggling with manual status override capabilities.
- **Inventory Management**: Full CRUD operations for regional catalogs, including robust image handling.
- **Regional Routing**: Intelligent order routing based on branch coverage and delivery zones.
- **Operational Analytics**: Integrated visual dashboards and charts utilizing `fl_chart`.

### 🔧 Technical Excellence
- **Domain-Driven API**: Deeply compartmentalized PHP backend isolating user, vendor, and admin scopes.
- **JWT Authentication**: Secure, stateless token-based sessions across all clients.
- **Strict Role-Based Access Control (RBAC)**: Ensuring complete data isolation across varying permission tiers.
- **State Management**: Reactive and localized UI updates powered by GetX.

---

## 🏗️ Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                      Order Ecosystem                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐                           ┌─────────────┐  │
│  │   Customer  │                           │ Admin/Vendor│  │
│  │  Mobile App │      [ FCM Push ]         │ Mobile App  │  │
│  │  (Flutter)  │ <-----------------------> │  (Flutter)  │  │
│  └──────┬──────┘                           └──────┬──────┘  │
│         │                                         │         │
│         │                                         │         │
│         └────────────────────┬────────────────────┘         │
│                              │                              │
│                     ┌────────▼────────┐                     │
│                     │   Backend API   │                     │
│                     │   (PHP/MySQL)   │                     │
│                     │                 │                     │
│                     │  - JWT Auth     │                     │
│                     │  - Routing Logic│                     │
│                     │  - RESTful      │                     │
│                     │  - File Upload  │                     │
│                     └────────┬────────┘                     │
│                              │                              │
│                     ┌────────▼────────┐                     │
│                     │  MySQL Database │                     │
│                     │                 │                     │
│                     │  - Catalogs     │                     │
│                     │  - Orders       │                     │
│                     │  - Users/Roles  │                     │
│                     │  - Regional Data│                     │
│                     └─────────────────┘                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Technology Stack

#### Frontend (Mobile Apps)
- **Framework**: Flutter 3.6+
- **State Management**: GetX
- **Storage**: GetStorage, Flutter Secure Storage
- **Networking**: HTTP package with interceptors
- **Push Notifications**: Firebase Cloud Messaging (FCM)
- **UI Components**: Material Design + Custom Animated Widgets

#### Backend API
- **Language**: PHP 8.0+
- **Database**: MySQL 8.0+
- **Architecture**: Domain-Driven RESTful Design
- **Authentication**: JWT Tokens
- **Media**: Native PHP file validation and localized secure storage

---

## 🚀 Getting Started

### Prerequisites

- **For Mobile Apps**:
  - Flutter SDK (>=3.6.0)
  - Dart SDK
  - Android Studio / VS Code
  - Valid Firebase configuration files (`google-services.json` / `GoogleService-Info.plist`)

- **For Backend**:
  - PHP (>=8.0)
  - MySQL (>=8.0)
  - Apache/Nginx Web Server

### Quick Start

#### 1. Clone the Repositories

```bash
# Clone the individual repositories
git clone https://github.com/your-org/backend.git
git clone https://github.com/your-org/order_app.git
git clone https://github.com/your-org/order_admin.git
```

#### 2. Setup Backend API

```bash
cd backend

# Configure database credentials in config directories
# Import the provided SQL schema
mysql -u username -p database_name < sql/schema.sql

# Set correct read/write permissions for media uploads
chmod -R 755 upload/

# Serve the backend
php -S localhost:8000
```

#### 3. Setup Customer & Admin Apps

```bash
cd order_app  # or cd order_admin

# Install dependencies
flutter pub get

# Ensure Firebase configs are placed in their respective platform folders
# Run the application
flutter run
```

---

## 📚 Documentation

### API Documentation

#### Base URL
```
https://api.your-domain.com/
```

#### Authentication
All protected endpoints require a JWT token:
```
Authorization: Bearer {your_jwt_token}
```

#### Standard Response Format

**Success:**
```json
{
  "status": "success",
  "data": { ... }
}
```

**Error:**
```json
{
  "status": "failure",
  "message": "Error description"
}
```

---

## 🎨 Features Overview

### Customer Mobile App

| Category | Features |
|----------|----------|
| **Shopping** | Vendor browsing, dynamic item catalogs, advanced cart calculations |
| **Account** | Tokenized registration, profile management, address book |
| **Orders** | Regional checkout validation, real-time pipeline tracking |
| **Notifications** | Firebase-powered push alerts for state transitions |

### Admin & Vendor App

| Category | Features |
|----------|----------|
| **Dashboard** | Revenue tracking, regional analytics, PDF reporting |
| **Catalog** | Full inventory CRUD, image upload handling |
| **Orders** | Enforcement of the Admin → Vendor accept sequence |
| **Vendor Ops**| Automated business hour tracking, manual status overrides |

### Backend API

| Feature | Description |
|---------|-------------|
| **Routing** | Zone-based branch mapping for regional orders |
| **Roles** | Complete isolation between Super Admins, Admins, Vendors, and Users |
| **Transactions**| Atomic database operations for concurrent checkout safety |

---

## 🔐 Security

### Implemented Measures

- **Authentication**: Stateless JWT implementation preventing session hijacking.
- **Client Security**: Code obfuscation and root detection enabled for production mobile builds.
- **SQL Injection Prevention**: Parameterized queries across all database interactions.
- **Data Isolation**: Strict RBAC rules preventing cross-tenant data leakage.

### Best Practices

- Always serve API endpoints over **HTTPS** in production environments.
- Keep Firebase keys securely excluded from public version control.

---

## 📱 Supported Platforms

### Client Applications

| Platform | Minimum Version | Tested Version |
|----------|----------------|----------------|
| Android | API 21 (Android 5.0) | API 34 (Android 14) |
| iOS | iOS 12.0 | iOS 17.0 |

---

## 🤝 Contributing

We welcome contributions from the community. Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting pull requests.

### Development Guidelines

- Adhere to the Flutter Style Guide and Dart best practices.
- Document complex UI state transitions inside GetX controllers.
- Ensure API changes do not break legacy mobile client versions.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Streamlining Delivery Operations with Precision**

<a href="https://play.google.com/store/apps/details?id=com.yasser.order">
  <img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" alt="Get it on Google Play" height="70">
</a>

[⬆ Back to Top](#order---comprehensive-delivery--e-commerce-platform)

</div>
