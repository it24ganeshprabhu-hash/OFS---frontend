# OFS Frontend Documentation

This README covers the frontend static UI for the OFS portal, located in `src/main/resources/static`.

## Frontend Overview

The frontend is implemented with pure HTML, CSS, and JavaScript. It is served as static resources by the Spring Boot backend and uses browser storage and REST calls to integrate with backend APIs.

### Main UI Pages

- `home.html` — landing page with key navigation to login, signup, and identity verification.
- `login.html` — user/admin login form with role selection and client-side session storage.
- `signup.html` — account registration form with Aadhaar input and onboarding guidance.
- `dashboard.html` — customer dashboard with balance card, quick actions, and AI assistant.
- `settings.html` — profile update, password change, photo upload, and QR generation.
- `passbook.html` — transaction history page with filtering, pagination, and PDF export.
- `trading.html` — paper trading interface with chart, order execution, and holdings view.
- `logs.html` — transaction log explorer for trading activity.
- `admin.html` — admin dashboard for user management, alerts, and support ticket handling.
- `aadhaar.html` — Aadhaar verification workflow with OTP and profile lookup.
- `services.html` — information page describing app service offerings.
- `about.html` — static about page.

## Frontend Features

- Responsive dashboard and landing pages with mobile-friendly navigation.
- Login/register flow using `localStorage` to hold active user ID and role.
- Aadhaar verification page with OTP lifecycle and verification feedback.
- Transaction UI for deposit, withdrawal, transfer, and passbook navigation.
- AI chat interface on dashboard to request financial advice.
- QR generation and scan-payment flow via the `/api` endpoints.
- Trading experience with live chart rendering and holdings management.
- Admin actions for creating users, updating status, support ticket replies, and alert dispatch.

## Client-side Technologies

- HTML5 + CSS3
- Vanilla JavaScript
- Google Fonts (`Inter`)
- `lightweight-charts` for the trading chart
- `jspdf` + `jspdf-autotable` for downloadable transaction PDF export

## Static Folder Structure

- `src/main/resources/static` — frontend entry points
- `static/home.html` — landing page
- `static/login.html` — login form
- `static/signup.html` — signup flow
- `static/dashboard.html` — customer dashboard
- `static/settings.html` — profile management
- `static/passbook.html` — passbook history
- `static/trading.html` — trading terminal
- `static/logs.html` — transaction logs
- `static/admin.html` — admin portal
- `static/aadhaar.html` — Aadhaar verification
- `static/services.html` — service overview
- `static/about.html` — about page

## Backend API Integration

The frontend expects the backend to be available at `http://localhost:8081`.

Key frontend API interactions:

- Authentication and user profile: `/login`, `/register`, `/get-details/{id}`, `/update`, `/update-photo`, `/get-profile-photo/{userId}`
- Transactions: `/deposit`, `/withdraw`, `/transfer`, `/apply-interest/{id}`, `/passbook/{id}`
- Aadhaar verification: `/aadhaar/start`, `/aadhaar/verifyOtp`
- AI guidance: `/api/ai/consult`
- QR support: `/api/generate-my-qr/{username}`, `/api/scan-pay`
- Trading: `/api/trade/execute`, `/api/trade/transfer-funds`, `/api/trade/withdraw-funds`, `/api/trade/portfolio-details`, `/api/trade/holdings`
- Support and admin: `/api/support/create`, `/api/support/admin/all`, `/api/support/admin/reply/{ticketId}`, `/api/alerts/send`, `/admin/update-status/{targetId}`, `/histories/admin/{adminId}`

> This frontend README does not cover backend implementation details.

## Running the Frontend

The static pages are loaded automatically when the Spring Boot backend runs.

To view the frontend locally:

1. Start the backend with `./mvnw spring-boot:run`.
2. Open `http://localhost:8081/home.html` in the browser.

Alternatively, you can open the HTML files directly in the browser, but the full experience requires the backend APIs to be available.

## Developer Notes

- `login.html` and `signup.html` use client-side state stored in `localStorage`.
- `dashboard.html` includes a notification drawer and AI chat popup.
- `settings.html` fetches profile data and supports QR image download.
- `passbook.html` and `logs.html` provide filtering and pagination.
- `trading.html` depends on `lightweight-charts` for a responsive price chart.
- `admin.html` includes creation and status management flows for users.

## Styling and UX

- Uses a clean teal/white financial theme.
- Responsive layout with mobile navigation in landing pages.
- Modal dialogs for actions such as transfers, support, and QR viewing.
- Action cards for quick access in the dashboard.

## Notes

- The static frontend relies on the backend for data and authentication.
- Keep the `API_URL` constant in the HTML pages aligned with the backend server URL.
- Do not store secrets in static files.
