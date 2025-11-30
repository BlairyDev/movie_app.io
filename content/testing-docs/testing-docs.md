+++
date = '2025-11-27T14:43:20-05:00'
draft = true
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




# Flutter Movie App – Acceptance Tests

## Week 2 – Login

### Login Feature

#### Scenario 1: Successful Login
- **Given** the user is on the login screen  
- **When** they enter a valid TMDB email and password  
- **And** tap **Login**  
- **Then** the user is authenticated  
- **And** navigated to the Home Screen  

#### Scenario 2: Invalid Login
- **Given** the user is on the login screen  
- **When** they enter invalid credentials  
- **And** tap **Login**  
- **Then** an error message appears  
- **And** the user stays on the login screen  

#### Scenario 3: Register (TMDB required)
- **Given** the user wants to create an account  
- **When** they tap **Register with TMDB**  
- **Then** the TMDB registration page opens  

#### Scenario 4: Forgot Password
- **Given** the user forgot their password  
- **When** they tap **Forgot Password**  
- **Then** the TMDB password reset page opens  

---

## Week 3 – Detail Pages (Start)

### Movie/TV Detail Page

#### Scenario 1: Display basic details
- **Given** the user opens a movie page  
- **Then** the app shows:  
  - Title  
  - Release date  
  - Synopsis  

#### Scenario 2: Display cast & crew
- **Given** the user is on the detail page  
- **Then** cast, crew, and production details appear  

#### Scenario 3: Show similar movies
- **Given** the user scrolls  
- **Then** similar or related movies are displayed  

#### Scenario 4: Add movie to list
- **Given** the user is viewing a movie  
- **When** they tap **Add to List**  
- **Then** the movie is added to their watchlist/favorites  

---

## Week 4 – Ratings & Reviews

### Ratings

#### Scenario 1: Add rating
- **Given** the user is logged in  
- **When** they give a rating (1–10)  
- **Then** the rating is saved  

#### Scenario 2: Edit/remove rating
- **Given** the user has rated a movie  
- **When** they edit or delete it  
- **Then** the rating updates correctly  

#### Scenario 3: Average rating
- **Given** multiple users rated a movie  
- **Then** the average rating reflects aggregated data  

---

### Reviews

#### Scenario 1: View reviews
- **Given** the user is on the detail page  
- **When** they scroll to reviews  
- **Then** reviews show username, timestamp, and rating  

#### Scenario 2: Sort reviews
- **Given** reviews are loaded  
- **When** user selects a sort mode  
- **Then** reviews reorder by:  
  - Newest  
  - Highest rated  

---

## Week 5 – Profiles & Detail Page Completion

### Profiles

#### Scenario 1: View profile
- **Given** the user opens their profile  
- **Then** they see:  
  - Watchlist  
  - Favorites  

#### Scenario 2: Logout
- **Given** the user is logged in  
- **When** they tap **Logout**  
- **Then** they return to login  
- **And** session data is cleared  

---

## Week 6 – Search, Filter, Watchlist

### Search

#### Scenario 1: Dynamic search
- **Given** the user types in the search bar  
- **Then** search results update dynamically  

### Filters

#### Scenario 1: Apply filters
- **Given** the user selects genre/year/rating/country filters  
- **Then** the results update  

#### Scenario 2: Reset filters
- **Given** filters are applied  
- **When** the user taps **Clear Filters**  
- **Then** all settings reset to default  

---

## Watchlist & Favorites

#### Scenario 1: Add/remove watchlist
- **Given** the user is on a movie detail page  
- **When** they tap **Add to Watchlist**  
- **Then** the movie is added  
- **When** they tap **Remove**  
- **Then** the movie is removed  

#### Scenario 2: Favorite a movie
- **Given** the user is on a detail page  
- **When** they tap **Favorite**  
- **Then** the movie is added to favorites  

---

## Week 7 – Ratings & Recommendations

### Ratings (final implementation)
- (Same as week 4 – must be complete & functional)

### Recommendations

#### Scenario 1: Display recommendations
- **Given** the user is logged in  
- **When** recommendations load  
- **Then** at least **10** suggestions appear  




+++
title = "Integration Testing"
weight = 20
+++

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

# 🧪 Integration Tests Performed

Below is a summary of the integration test scenarios implemented.

---

## ✔ 1. Login → HomeScreen Flow

**Purpose:**  
Confirm that valid TMDB credentials successfully navigate the user to the Home screen.

**Actions Performed:**

- Enter username  
- Enter password  
- Tap Login button  
- Wait for async processes  
- Validate that `HomeScreen` appears  

**Why it matters:**  
This is the central entry point to the entire app.

---

## ✔ 2. Profile Navigation (Home → Profile → Back)

**Purpose:**  
Verify that users can open their profile and return to the home screen.

**Actions Performed:**

- Tap Profile icon  
- Confirm `ProfileScreen` is displayed  
- Navigate back  
- Confirm `HomeScreen` is visible  

**Why it matters:**  
Profile contains watchlist, favorites, and logout features. Navigation must be stable.

---

## ✔ 3. Carousel Movie → Movie Detail Screen

**Purpose:**  
Ensure that TMDB API results load correctly and that tapping a movie navigates to the detail page.

**Actions Performed:**

- Wait for carousel movie cards to load  
- Tap the center of the carousel  
- Confirm detail-screen elements such as:  
  - “Toggle Watchlist”  
  - “See Reviews”  
- Navigate back to Home  

**Why it matters:**  
This verifies the entire end-to-end flow:  
API → Carousel UI → Tap → Movie Detail page.

---

## ✔ 4. Register and Forgot Password Buttons

**Purpose:**  
Check that both TMDB authentication actions are available on the login screen.

**Actions Performed:**

- Look for “Need an account? Register”  
- Look for “Forgot Password? Reset Password”  

**Why it matters:**  
These are required in the Week 2 login features.

---

# 📂 Feature Coverage

The integration tests directly support key project requirements:

| Feature | Requirement Verified | Test |
|--------|----------------------|------|
| Login | TMDB login via username/password | Login success test |
| Profile | User can access profile and return | Profile navigation test |
| Movie Detail | Movies load + detail page navigation works | Carousel → detail test |
| TMDB Auth | Register and Forgot Password links visible | Buttons visibility test |

---

# 🏆 Importance of Integration Testing

These tests ensure:

- Correct screen-to-screen transitions  
- Stable user experience  
- Accurate UI behavior after async loads  
- Functional API integration  
- Navigation stack reliability  
- Early detection of breaking changes (supports regression testing)

They verify that the app behaves properly as a complete system, not just as individual widgets or functions.

---

# 📌 Summary

The Movie App’s integration tests successfully validated:

- Login flow  
- Profile navigation  
- Carousel interaction  
- Movie detail navigation  
- Presence of TMDB register/reset password options  

This confirms the app’s core flows operate correctly and provides confidence for future updates, UI changes, and feature additions.

