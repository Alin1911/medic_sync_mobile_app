# MedicSyncApp

MedicSyncApp is a Flutter mobile application focused on digital prescription management and pharmacy discovery.  
It provides a clean patient experience for authentication, viewing active prescriptions, validating QR-based prescriptions, and finding nearby pharmacies with route guidance.

## Why this project matters

This project demonstrates practical product thinking and end-to-end mobile engineering:
- Healthcare-oriented user flows (authentication, profile, medication data)
- Real API integration with token-based auth and protected endpoints
- Location-aware mapping experience (Google Maps + Places + Directions)
- Structured codebase with clear separation between UI, services, and models

## Core features

- **Login flow** with token persistence using `SharedPreferences`
- **Dashboard overview** with prescription status cards
- **My Prescriptions** screen with:
  - API-fetched prescriptions
  - medication lists
  - QR code rendering for pharmacy validation
  - visual state for valid/invalid QR codes
- **Nearby Pharmacies** map module with:
  - current location detection
  - nearby pharmacy markers
  - open-now and minimum-rating filters
  - route drawing using polyline decoding
- **Profile module** for reading and updating patient profile details

## Architecture

The app follows a lightweight layered structure:

- `lib/screens/` → presentation layer (UI, navigation, interactions)
- `lib/services/` → data/access layer (HTTP calls, auth token usage)
- `lib/models/` → domain/data models for JSON mapping

### Main navigation flow

1. App starts in `main.dart`
2. User lands on `LoginScreen`
3. Successful login stores `access_token` and routes to `DashboardScreen`
4. Dashboard uses tab-based navigation:
   - Dashboard summary
   - My Prescriptions
   - Nearby Pharmacies
   - Profile

## Technology stack

- **Framework:** Flutter (Dart)
- **State approach:** Stateful widgets + `FutureBuilder`
- **Networking:** `http`
- **Local storage:** `shared_preferences`
- **Maps & geo:** `google_maps_flutter`, `geolocator`, Google Places API, Google Directions API
- **QR rendering:** `qr_flutter`
- **Typography/UI:** `google_fonts`
- **Linting:** `flutter_lints`

## API integration

The mobile app currently expects a backend running locally for emulator usage:
- Base auth endpoint: `http://10.0.2.2:8001/oauth/token`
- Base API endpoint: `http://10.0.2.2:8001/api`

Used endpoints include:
- `POST /oauth/token`
- `GET /api/prescriptions`
- `GET /api/me`
- `PUT /api/me`

## Project structure

```text
lib/
  main.dart
  models/
    prescription_models.dart
  screens/
    login_screen.dart
    dashboard_screen.dart
    my_prescriptions_screen.dart
    nearby_pharmacies_screen.dart
    profile_screen.dart
  services/
    auth_service.dart
    prescription_service.dart
    user_service.dart
```

## Getting started

### 1) Prerequisites
- Flutter SDK (matching Dart SDK constraints in `pubspec.yaml`)
- Android Studio / Xcode (depending on target platform)
- A running backend compatible with the listed endpoints
- Google Maps API key with required services enabled

### 2) Install dependencies

```bash
flutter pub get
```

### 3) Run the app

```bash
flutter run
```

## Quality and maintainability notes

- Uses typed models for safer JSON parsing in the prescriptions module
- Keeps network logic out of UI widgets via service classes
- Includes Flutter lint configuration via `analysis_options.yaml`

## Security note

For production readiness:
- Move API keys and sensitive credentials to secure environment configuration
- Avoid hardcoding client secrets in source files
- Use secure token lifecycle and refresh handling

## Future improvements

- Introduce state management (e.g., Provider/BLoC/Riverpod) for scalability
- Add robust test coverage (unit, widget, integration)
- Centralize API configuration and environment switching (dev/staging/prod)
- Improve error handling and offline support
