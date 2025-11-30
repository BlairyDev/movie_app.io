+++
menus = 'main'
title = 'Architecture Docs'
+++

Github Link: https://github.com/BlairyDev/movie_app

# App Architecture


![App Architecture](https://blairydev.github.io/movie_app.io/software-architecture.png)



## Overview
We will grab all our movie data in the [Tmdb API](https://developer.themoviedb.org/docs/getting-started). The API already offers login and this means users has the ability to add, remove, update, and rate movies.


## App Design Pattern (MVVM)

![MVVM](https://journaldev.nyc3.cdn.digitaloceanspaces.com/2018/04/android-mvvm-pattern.png)

We are going to use MVVM Design pattern to make it easier for collaborations, scalable, and testing.

 - I will create another tutorial file on how everything works with the codebase


# 🎬 Movie App – Flutter

A Flutter-based movie browsing application that allows users to log in, explore popular movies, open detailed pages, and manage their profile. The app uses MVVM architecture with Provider for state management and integrates with a movie API for real-time data.

---

##  Features

-  **User Login & Logout**
-  **Browse Popular Movies**
-  **Search for Movies**
-  **Movie Detail Page**
-  **Profile Screen**
-  **Filter Sheet for Movie Sorting**
-  **Carousel Slider for Featured Movies**

---

## 🗂️ Project Structure (Architecture)

This project follows **MVVM** (Model–View–ViewModel) with clean folder organization.

```
lib/
 ├── data/
 │    ├── models/         # Movie, User models
 |    ├──repositories/
 │    └── services/       # API services
 ├── view/
 │    ├── home_screen.dart
 │    ├── movie_detail_screen.dart
 │    ├── profile_screen.dart
 │    └── filter_sheet.dart
 │    └── review_screen.dart
 │    └── login_screen.dart
 ├── view_models/         # HomeViewModel, ReviewViewModel, etc.
 ├── di/           # GetIt Dependency Injection
 └── main.dart
```

**Key Concepts Used:**
- **Provider** for state management
- **GetIt** for dependency injection  
- **MVVM** to separate UI and logic  
- **HTTP/REST API** integration  

---

## 🛠️ Installation & Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/movie_app.git
```

2. Install dependencies:
```bash
flutter pub get
```

3.  If your project needs an API key, create:
```
lib/.env
```
and add:
```dart
API_KEY=api_key="YOUR_API_KEY"
//for testing
TEST_PASSWORD="TMDB_PASSWORD"
TEST_USERNAME="USERNAME"

4. Run the app:
```bash
flutter run
```

```

## 🧰 Technologies Used

- Flutter 3.x  
- Dart  
- Provider  
- HTTP  
- Carousel Slider  
- GetIt (if DI used)   

---

## 🐞 Known Issues / Limitations

- Some API requests may load slowly  
- Error handling can be improved  
- Profile editing is minimal
- UI issues in some size of screen

---

## 🔮 Future Improvements

- Build improved animations  
- Improve UI
- Add more features
- Add our own server

---

## 👨‍💻 Members

**Blair**  
**Aj**
**Parker**   
**Cambden** 
**Preston** 

---
