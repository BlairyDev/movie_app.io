+++
date = '2025-11-27T14:43:20-05:00'
title = 'Testing Docs'
menus = 'main'
+++

# Regression Testing

Regression testing ensures that new features do not break previously working functionality.

For this project, full regression testing was **not implemented** due to time limitations and sprint priorities.

However, the team performed **informal manual checks** after major features were added, including:
- Login still works after UI updates
- Navigation continues to work
- Detail pages still load correctly
- Search and filters still respond as expected
- Able to add and remove in watchlist and favorites

Formal automated regression tests (scripts or automated suites) were planned but not executed in this version of the project.




# 📘 Integration Testing

## Overview

Integration testing ensures that **multiple components of the Movie App work together as a complete system**.  
Where unit tests focus on functions and widget tests focus on UI components, integration tests simulate **real user behavior across screens, navigation, API calls, and asynchronous operations**.

These tests validate the main user flows and confirm that the app behaves correctly from start to finish.

---

# 🎯 Goals of Integration Testing

The integration tests in this project were designed to verify:

- The login flow using TMDB authentication  
- Navigation between Home, Profile, and Movie Detail screens  
- UI responsiveness after API data loads  
- Carousel interaction and movie selection  
- Presence of required TMDB register/forgot password options  
- Stable asynchronous behavior during navigation and loading

---

# Movie App - Integration Testing Documentation

## Overview

This document provides comprehensive information about the integration tests for the Movie App. The test suite validates critical user flows including authentication, navigation, search functionality, profile management, and logout operations.

## Prerequisites

### Environment Setup

1. **Create a TMDB Account**
   - Sign up at [The Movie Database (TMDB)](https://www.themoviedb.org/)
   - Generate API credentials

2. **Configure Environment Variables**
   
   Create a `.env` file in the root directory with the following credentials:
   ```env
   TEST_USERNAME=your_tmdb_username
   TEST_PASSWORD=your_tmdb_password
   ```

3. **Install Dependencies**
   ```bash
   flutter pub get
   ```

## Running the Tests

### Run All Tests
```bash
flutter test integration_test/app_test.dart
```


## Test Suite Structure

The integration tests are organized into the following categories:

### 1. Login and Navigation Tests

Tests that verify user authentication and basic navigation flows.

| Test Name | Description | Key Validations |
|-----------|-------------|-----------------|
| `Login success navigates to home screen` | Validates successful login flow | - Username/password entry<br>- Login button functionality<br>- Navigation to home screen |
| `ProfileScreen then back` | Tests profile navigation | - Navigation to profile screen<br>- Back navigation to home |
| `Register and forgot password buttons are present` | Verifies auxiliary buttons | - "Need an account? Register" button<br>- "Forgot Password? Reset Password" button |

### 2. Search Functionality Tests

Tests covering the movie search feature and its various states.

| Test Name | Description | Key Validations |
|-----------|-------------|-----------------|
| `Search icon opens search bar` | Validates search UI toggle | - Search icon visibility<br>- Search bar appearance<br>- Cancel icon replaces search icon |
| `Search for movies and display results` | Tests search execution | - Search query entry<br>- Results display in list view<br>- Card widgets presence |
| `Search with no results shows message` | Tests empty state | - No results message display<br>- Proper handling of non-existent queries |
| `Cancel search returns to carousel view` | Tests search cancellation | - Cancel icon functionality<br>- Return to carousel view<br>- Search icon restoration |
| `Multiple searches can be performed consecutively` | Tests sequential searches | - Multiple search executions<br>- Results update correctly |
| `Search hint text is displayed` | Validates placeholder text | - "Search movies..." hint text visibility |
| `Profile and search icons coexist properly` | Tests icon state management | - Both icons visible simultaneously<br>- Proper icon transitions |
| `Loading indicator shows during search` | Tests loading states | - Loading indicator appearance<br>- Results or message display after loading |

### 3. Profile Screen Tests

Tests for profile screen functionality and tab navigation.

| Test Name | Description | Key Validations |
|-----------|-------------|-----------------|
| `Navigate to profile screen from home` | Tests profile access | - Profile icon functionality<br>- Profile screen elements visibility |
| `Display watchlist movies by default` | Tests default view | - Watchlist tab selection<br>- Movies/TV Shows sub-tabs |
| `Switch between Movies and TV Shows in watchlist` | Tests tab switching | - TV Shows tab navigation<br>- Movies tab navigation<br>- Content or empty state display |
| `Navigate to Favorites tab` | Tests favorites section | - Favorites tab access<br>- Sub-tabs visibility |
| `Navigate to Reviews tab` | Tests reviews section | - Reviews tab access<br>- "Coming Soon" message display |

### 4. Logout Tests

Tests for logout functionality and session management.

| Test Name | Description | Key Validations |
|-----------|-------------|-----------------|
| `Logout and navigate to login screen` | Tests logout flow | - Logout button functionality<br>- Navigation to login screen<br>- Login fields presence |
| `Clear session data on logout` | Tests data cleanup | - Session data removal<br>- Profile data unavailability |
| `Cannot navigate back after logout` | Tests navigation stack | - Back navigation prevention<br>- Route removal verification |

### 5. Error Handling Tests

Tests for error states and edge cases.

| Test Name | Description | Key Validations |
|-----------|-------------|-----------------|
| `Display error message when watchlist fails to load` | Tests error UI | - Error message display<br>- Retry button functionality |
| `Display empty state when no movies found` | Tests empty states | - Empty state message<br>- Proper UI feedback |

## Key Features Tested

### Authentication Flow
- Login with valid credentials
- Navigation after successful login
- Session persistence

### Search Functionality
- Search bar toggle
- Movie search execution
- Results display (list view)
- Empty state handling
- Search cancellation
- Multiple consecutive searches
- Loading states

### Navigation
- Home to Profile navigation
- Back navigation
- Tab switching within Profile
- Logout navigation with route clearing

### Profile Management
- Watchlist display
- Favorites access
- Reviews section
- Movies/TV Shows toggle
- Tab navigation

### Error Handling
- Network error recovery
- Empty state messages
- Retry mechanisms

## Helper Functions

### `loginAndNavigateToHome(WidgetTester tester)`

A reusable helper function that:
1. Launches the app
2. Retrieves credentials from `.env`
3. Performs login
4. Waits for navigation to home screen
5. Waits for movies to load

**Usage:**
```dart
await loginAndNavigateToHome(tester);
```

## Test Execution Flow

Each test follows this general pattern:

1. **Setup**: Reset GetIt instance for clean state
2. **Arrange**: Launch app and perform necessary navigation
3. **Act**: Execute the test action (tap, enter text, etc.)
4. **Assert**: Verify expected outcomes using `expect()`
5. **Cleanup**: Automatic via `setUp()` hook

## Important Notes

### Timing Considerations

The tests use various wait strategies:
- `pumpAndSettle()`: Wait for all animations to complete
- `pump(Duration)`: Wait for a specific duration
- Multiple pumps for async operations

### Widget Keys

The app uses specific keys for testing:
- `usernameField`: Username input field
- `passwordField`: Password input field
- `loginButton`: Login submit button
- `homeScreen`: Home screen identifier

### State Management

- **GetIt**: Dependency injection container (reset before each test)
- **Provider**: State management (HomeViewModel, ProfileViewModel)

## Troubleshooting

### Tests Failing Due to Timeout
- Increase wait durations in `pump(Duration(seconds: X))`
- Check network connectivity for API calls

### Widget Not Found
- Verify widget keys match implementation
- Use `find.text()`, `find.byType()`, or `find.byIcon()` as alternatives
- Check if widget is scrollable and needs `scrollUntilVisible()`

### Authentication Failures
- Verify `.env` file exists and contains valid credentials
- Ensure TMDB account is active
- Check API rate limits

### GetIt Errors
- Ensure `setUp()` is properly resetting GetIt
- Verify dependencies are registered correctly in `main.dart`

## Best Practices

1. **Isolation**: Each test should be independent
2. **Cleanup**: Use `setUp()` to ensure clean state
3. **Assertions**: Use descriptive error messages
4. **Wait Strategies**: Balance between speed and reliability
5. **Real User Flows**: Test complete user journeys, not just individual actions

## Continuous Integration

To run these tests in CI/CD:

```yaml
# Example GitHub Actions workflow
- name: Run Integration Tests
  run: |
    flutter test integration_test/app_test.dart
```

Ensure environment variables are securely stored in CI/CD secrets.

## Test Coverage Summary

- ✅ Authentication (3 tests)
- ✅ Search Functionality (9 tests)
- ✅ Profile Navigation (5 tests)
- ✅ Logout Operations (3 tests)
- ✅ Error Handling (2 tests)

**Total Tests**: 22

## Future Test Additions

Consider adding tests for:
- Movie detail view
- Add to watchlist functionality
- Add to favorites functionality
- Rating submission
- TV show search and navigation
- Offline behavior
- Network error recovery
- Invalid login credentials
- Form validation

---

## Contact & Support

For questions or issues with the test suite, please refer to the project's issue tracker or documentation.

---

# 📌 Summary

The Movie App’s integration tests successfully validated:

- Login flow  
- Profile navigation  
- Carousel interaction  
- Movie detail navigation  
- Presence of TMDB register/reset password options  

# Acceptance Tests – Movie App

## 1. Login & Authentication

### Scenario 1: Successful Login
- **Given** the user is on the Login screen  
- **When** they enter a valid TMDB email and password  
- **And** tap **Login**  
- **Then** the user is authenticated  
- **And** redirected to the Home screen  

### Scenario 2: Invalid Login
- **Given** the user is on the Login screen  
- **When** they enter an invalid email or password  
- **And** tap **Login**  
- **Then** an error message is displayed  
- **And** the user remains on the Login screen  

### Scenario 3: Redirect to Register (TMDB Required)
- **Given** the user is on the Login screen  
- **When** they tap **Register**  
- **Then** the app redirects them to the TMDB registration page  

### Scenario 4: Forgot Password
- **Given** the user is on the Login screen  
- **When** they tap **Forgot Password**  
- **Then** the user is redirected to the TMDB password recovery page  


## 2. Movie & TV Detail Pages

### Scenario 1: Display Movie Details
- **Given** the user opens a movie detail page  
- **Then** the app displays the title, release date, and synopsis  

### Scenario 2: Add to Watchlist
- **Given** the user is on the detail page  
- **When** they tap **Add to Watchlist**  
- **Then** the movie is added to their watchlist  
- **And** the UI updates to reflect the change  

### Scenario 3: Remove from Watchlist
- **Given** the movie is already in the user’s watchlist  
- **When** they tap **Remove from Watchlist**  
- **Then** the movie is removed from the watchlist  

### Scenario 4: Add to Favorites
- **Given** the user is on the detail page  
- **When** they tap **Add to Favorites**  
- **Then** the movie is added to their favorites  

### Scenario 5: Remove from Favorites
- **Given** the movie is in the favorites list  
- **When** they tap **Remove from Favorites**  
- **Then** the movie is removed from favorites  


## 3. Ratings

### Scenario 1: Add Rating
- **Given** the user is on a detail page  
- **When** they submit a rating from 1–10  
- **Then** the rating is saved and displayed  

### Scenario 2: Edit Rating
- **Given** the user already rated the movie  
- **When** they update the rating  
- **Then** the new rating replaces the old one  

### Scenario 3: Remove Rating
- **Given** the user has a rating on the movie  
- **When** they remove their rating  
- **Then** the rating is deleted  


## 4. Reviews

### Scenario 1: View Reviews
- **Given** the user is on a detail page  
- **When** reviews are available  
- **Then** each review displays username, timestamp, and rating (if provided)  

### Scenario 2: Sort Reviews
- **Given** reviews are displayed  
- **When** the user chooses a sort option (newest, highest rated)  
- **Then** the reviews reorder accordingly  


## 5. Profiles

### Scenario 1: Display Profile
- **Given** the user opens their profile  
- **Then** the app displays the user’s watchlist and favorites  

### Scenario 2: Logout
- **Given** the user is logged in  
- **When** they tap **Logout**  
- **Then** they are signed out  
- **And** redirected to the Login screen  


## 6. Search & Filters

### Scenario 1: Search by Title/Keyword/Cast
- **Given** the user is on the Search screen  
- **When** they type a term  
- **Then** results update dynamically  
- **And** movies/TV shows matching title, keyword, or cast appear  

### Scenario 2: Apply Filters
- **Given** the user opens Filters  
- **When** they choose genre, year, rating, or country  
- **Then** the results update to match the filters  

### Scenario 3: Clear Filters
- **Given** filters are active  
- **When** the user taps **Reset/Clear Filters**  
- **Then** all filters return to default  
- **And** the search results reset  


## 7. Watchlist & Favorites (Global Behavior)

### Scenario 1: Watchlist Toggle
- **Given** the user views a movie  
- **When** they toggle Watchlist  
- **Then** the movie is added or removed accordingly  

### Scenario 2: Favorites Toggle
- **Given** the user views a movie  
- **When** they toggle Favorites  
- **Then** the movie is added or removed accordingly  


## 8. Recommendations

### Scenario 1: Display Recommendations
- **Given** the user is on the Home or Detail page  
- **When** recommendations load  
- **Then** at least 10 suggested movies/TV shows are displayed  


## 9. UI Requirements

### Scenario 1: General UI Rendering
- **Given** the user navigates through the app  
- **Then** all pages must display intended UI components  
- **And** all interface elements must render correctly  


