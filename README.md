# Laravel Full-Stack Assessment: Employee TimeFlow System

**Role:** Developer Intern  
**Deadline:** 7 Days from Date of Assignment  
**Focus:** Routing, Middleware, Eloquent Relationships, Blade Components

---

## ⛔ Strict Tech Stack Rules

To ensure we are testing your specific knowledge of the core Laravel ecosystem, you must adhere to the following constraints. **Any deviation will result in disqualification.**

1.  **Framework:** **Laravel 12.x** (Must use the latest version).
2.  **Frontend:** **Blade Templates ONLY.**
    * ❌ **NO** React, Vue, Alpine.js, or Livewire.
    * ❌ **NO** jQuery or raw JavaScript (unless strictly for simple DOM manipulation).
3.  **Styling:** **Tailwind CSS ONLY.**
    * ❌ **NO** Bootstrap, Bulma, or custom CSS files.
    * You must use Tailwind utility classes directly in your Blade files or Components.
4.  **Database:** MySQL.
5.  **Security:** **All app routes must be Password Protected.**
    * Public access to the dashboard or attendance actions is strictly forbidden.

---

## 🎯 Project Overview

You are tasked with building **TimeFlow**, a simple internal tool that allows employees to track their daily work hours. The system must track when an employee starts work (Check In) and when they finish (Check Out).

The goal of this assignment is **not just to make it work**, but to demonstrate clean code architecture, proper usage of Laravel’s MVC structure, and the implementation of **reusable Blade components**.

---

## 🛠 Functional Requirements

### 1. Authentication (Strict)
- Use **Laravel Breeze** (Blade stack) or standard UI Auth.
- **Middleware:** All operational routes must be protected using the `auth` middleware. If a guest tries to visit `/dashboard`, they must be redirected to the login page.

### 2. The Dashboard (Home Screen)
- The main view should display the **Current Status** of the user.
    - If the user is **Offline**: Show a "Check In" button.
    - If the user is **Active**: Show a "Check Out" button and a timer (optional) or start time.
- Below the status, display a **History Table** showing the user's past 5 attendance records.

### 3. Logic Constraints
- A user **cannot** check in if they are already checked in.
- A user **cannot** check out if they are not currently working.
- The history table should calculate total hours worked for completed sessions.

---

## 💻 Technical Specifications

### A. Database Schema
You will need a new migration for an `attendances` table.

| Column Name | Type | Modifiers | Description |
| :--- | :--- | :--- | :--- |
| `id` | BigInt | PK | Primary Key |
| `user_id` | BigInt | FK | Links to `users` table |
| `check_in` | Timestamp | | Date & Time work started |
| `check_out` | Timestamp | Nullable | Date & Time work ended |
| `created_at` | Timestamp | | |
| `updated_at` | Timestamp | | |

> **Requirement:** Define the `hasMany` relationship in the `User` model and the `belongsTo` relationship in the `Attendance` model.

### B. Routes & Controllers
Avoid using closures in your web routes. Use a dedicated `AttendanceController`.
**All routes below must be wrapped in a Route Group with `middleware('auth')`.**

- `GET /dashboard` → Logic to determine if user is currently working.
- `POST /attendance/check-in` → Creates a new record.
- `PATCH /attendance/check-out` → Updates the *active* record with the current timestamp.

### C. Blade & Components (Critical)
**You are required to create and use the following reusable Blade Components.** Do not repeat Tailwind classes in your main views.

1.  **`<x-status-badge :status="$status" />`**
    - Takes a status string ('active' or 'offline').
    - Renders a Tailwind-styled badge (e.g., `bg-green-100 text-green-800` for active).
    
2.  **`<x-action-button :type="$type" />`**
    - A button component used for submitting the forms.
    - Must accept a type (e.g., 'primary' for Check In, 'danger' for Check Out).

3.  **`<x-attendance-table :history="$history" />`**
    - A component that accepts the collection of past attendance records and renders the table.

---

## 🧪 Grading Rubric

We will be looking for the following in your code:

- [ ] **Security:** Are routes truly protected? (We will try to access `/dashboard` in Incognito mode to see if it redirects to Login).
- [ ] **Tailwind Usage:** Proper use of utility classes (e.g., `flex`, `justify-between`, `p-4`).
- [ ] **Code DRY-ness:** logic should not be repeated in views; use components.
- [ ] **Data Integrity:** The app must prevent "Double Check-ins".
- [ ] **Eloquent Usage:** usage of Carbon for dates (e.g., `$attendance->check_in->diffForHumans()`).

---

**Good Luck!**
