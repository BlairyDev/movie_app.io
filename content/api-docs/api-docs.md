+++
date = '2025-11-27T14:27:02-05:00'
draft = true
title = 'Api Docs'
menus = 'main'
+++

# 🎬 Movie App – API Documentation

This document describes the **API services** used in the Movie App project. The app uses **TMDB API** and custom API service classes in Flutter (`TmdbApiService` and `TmdbAuthService`).


For more information about the Third Party here is a [link](https://developer.themoviedb.org/docs/getting-started)

---

## 🔹 Base URLs & Authorization

- **TMDB API Base URL:** `https://api.themoviedb.org/3`  
- **API Key:** Stored in `.env` → `API_KEY`  
- **Authorization:** Bearer token in `.env` → `ACCESS_TOKEN`  

**Headers for authenticated requests:**
```http
Authorization: Bearer <ACCESS_TOKEN>
Content-Type: application/json
```

---

## 🔹 TmdbApiService Endpoints

### 1️⃣ Fetch Upcoming Movies
- **Function:** 
```dart
fetchUpcomingMovies()
```
- **Method:** GET  
- **Endpoint:** `/movie/upcoming`  
- **Parameters:**  
  - `api_key`  
  - `language=en-US`  
- **Response:** JSON containing upcoming movie details

---

### 2️⃣ Search Movies
- **Function:** 
```dart
fetchSearchMovies(String title, {int page = 1})
```
- **Method:** GET  
- **Endpoint:** `/search/movie`  
- **Query Parameters:**  
  - `api_key`  
  - `language=en-US`  
  - `query` → movie title  
  - `page` → page number  
- **Response:** JSON with search results

---

### 3️⃣ Fetch Movie Reviews
- **Function:** 
```dart
fetchMovieReviews(int movieId, {int page = 1})
```
- **Method:** GET  
- **Endpoint:** `/movie/{movieId}/reviews`  
- **Parameters:**  
  - `api_key`  
  - `language=en-US`  
  - `page`  
- **Response:** JSON containing reviews for the movie

---

### 4️⃣ Fetch Movie/TV Watchlist
- **Functions:**  
```dart
fetchMovieWatchlist(int accountId, String sessionId)
fetchTvWatchlist(int accountId, String sessionId)
```
- **Method:** GET  
- **Endpoint:**  
  - `/account/{accountId}/watchlist/movies`  
  - `/account/{accountId}/watchlist/tv`  
- **Authentication required:** `session_id` in query, Bearer token in headers  
- **Response:** JSON list of movies/TV shows in watchlist

---

### 5️⃣ Fetch Genres
- **Function:** 
```dart
fetchGenres()
```
- **Method:** GET  
- **Endpoint:** `/genre/movie/list`  
- **Response:** JSON with all movie genres

---

### 6️⃣ Fetch Languages
- **Function:** 
```dart
fetchLanguages()
```
- **Method:** GET  
- **Endpoint:** `/configuration/languages`  
- **Response:** JSON array of supported languages

---

### 7️⃣ Discover Movies
- **Function:** 
```dart
discoverMovies(Map<String, String> queryParams)
```
- **Method:** GET  
- **Endpoint:** `/discover/movie`  
- **Query Parameters:** Customizable (e.g., `sort_by`, `with_genres`)  
- **Response:** JSON with filtered movie results

---

### 8️⃣ Favorites
- **Functions:**  
```dart
getFavoritesMoviesList(int? accountId, String? sessionId)
getFavoritesTVList(int? accountId, String? sessionId)
addToFavoritesMoviesList(...)
```
- **POST Body Example:**
```json
{
  "media_type": "movie",
  "media_id": 12345,
  "favorite": true
}
```

---

### 9️⃣ Watchlist
- **Functions:**  
```dart
getMovieWatchlist(int? accountId, String? sessionId)
getTvWatchlist(int? accountId, String? sessionId)
addToWatchlist(...)
```
- **POST Body Example:**
```json
{
  "media_type": "movie",
  "media_id": 12345,
  "watchlist": true
}
```

---

### 🔟 Recommendations
- **Function:** 
```dart
getRecommendationsMoviesList(int? movieId)
```
- **Method:** GET  
- **Endpoint:** `/movie/{movieId}/recommendations`  
- **Response:** JSON with recommended movies for the given movie ID

---

## 🔹 TmdbAuthService Endpoints

### 1️⃣ Fetch Request Token
- **Function:** 
```dart
fetchRequestToken()
```
- **Method:** GET  
- **Endpoint:** `/authentication/token/new`  
- **Response:** JSON with `request_token`

---

### 2️⃣ Validate Login
- **Function:** 
```dart
validateLogin(String username, String password, String requestToken)
```
- **Method:** POST  
- **Endpoint:** `/authentication/token/validate_with_login`  
- **Body:**
```json
{
  "username": "your_username",
  "password": "your_password",
  "request_token": "<token>"
}
```
- **Response:** JSON with `success` boolean

---

### 3️⃣ Create Session
- **Function:** 
```dart
createSession(String validatedRequestToken)
```
- **Method:** POST  
- **Endpoint:** `/authentication/session/new`  
- **Body:**
```json
{
  "request_token": "<validated_token>"
}
```
- **Response:** JSON with `session_id`

---

### 4️⃣ Fetch Account Details
- **Function:** 
```dart
fetchAccountDetails(String sessionId)
```
- **Method:** GET  
- **Endpoint:** `/account`  
- **Query Parameter:** `session_id`  
- **Response:** JSON with account info (ID, username, etc.)

---

## 🔹 Notes & Best Practices

- All authenticated endpoints require **`session_id` and Bearer token**.  
- Pagination is supported via **`page`** query parameter.  
- POST requests require **`Content-Type: application/json`**.  
- Exceptions are thrown if HTTP response status is not 200 OK.

---

