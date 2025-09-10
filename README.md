# 🎵 Music Manager

**Music Manager** is a Django-based music management system similar to Spotify or YouTube Music. Users can browse songs and albums, create playlists, like or favorite tracks, and follow artists. This project is built with **Django** and follows the **MVT architecture**.

---

## Repository Info

- **Repository Name:** `music-manager`  
- **Short Description:** A Django-based music management system with users, playlists, and artists.  
- **Author:** [Your Name]  
- **License:** MIT

---

## 1. Project Overview

**Goals:**
- Learn Django and MVT architecture
- Build a practical system with multiple roles and user interactions
- Prepare for future enhancements and advanced features

---

## 2. Key Features

### Roles
- **User:** Sign up & login, browse songs and albums, create/manage playlists, like tracks/albums, add tracks to favorites, follow artists or public playlists  
- **Artist:** All User capabilities + manage albums/tracks + edit artist profile  
- **Admin:** All User capabilities + manage users, music, genres, playlists + view reports/statistics

---

## 3. Core Models

### Users & Roles
- `User`: username, email, password, profile image, city, age  
- `Artist` (1-to-1 with User): bio, country  
- `Admin` (1-to-1 with User): permissions, manage users/music  

### Music
- `Artist`  
- `Album`: title, artist (FK), release_date, cover_image  
- `Track`: title, album (FK optional), artist (FK), genre (FK), duration, audio_file  
- `Genre`: name  

### User Interactions
- `Playlist`: name, user (FK), tracks (ManyToMany), is_public  
- `Like`: user (FK), track or album (generic relation), created_at  
- `Favorite`: user (FK), tracks (ManyToMany)  
- `Follow`: user (FK), artist or playlist (generic relation), follow_date  

---

## 4. ERD Overview (Text-based)

User --1:1--> Artist
User --1:1--> Admin
Artist --1:N--> Album
Album --1:N--> Track
Artist --1:N--> Track
Track --1:1--> Genre
Playlist --M:N--> Track
User --1:N--> Playlist
User --M:N--> Like --> Track/Album
User --M:N--> Favorite --> Track
User --M:N--> Follow --> Artist/Playlist

---

## 5. Layered Architecture (Text-based)

┌─────────────────────────────┐
│ Presentation Layer │
│ - Django Views, Templates │
│ - REST API Endpoints │
│ Apps: users, music, playlists, search, admin_panel
└─────────────▲───────────────┘
│
│ Calls / Business Logic
┌─────────────┴───────────────┐
│ Business Logic Layer │
│ - Services / Managers │
│ - Rules: Like, Follow, Playlist, Favorite
│ Apps: users, music, playlists
└─────────────▲───────────────┘
│
│ Access Data
┌─────────────┴───────────────┐
│ Data Access Layer │
│ - Django Models / ORM │
│ Models: User, Artist, Admin, Album, Track, Genre, Playlist, Like, Favorite, Follow
└─────────────▲───────────────┘
│
│ Storage / Media
┌─────────────┴───────────────┐
│ Infrastructure Layer │
│ - Audio / Media Storage │
│ - Reporting / Analytics │
│ - External Services (optional)
└─────────────────────────────┘

---

## 6. App Structure

music_manager_project/
│
├── users/ # User, Artist, Admin
├── music/ # Artist, Album, Track, Genre
├── playlists/ # Playlist, Like, Favorite
├── search/ # Search & filter functionality
├── admin_panel/ # Admin management
├── templates/ # HTML templates
├── static/ # CSS, JS, Images
├── media/ # Uploaded audio and images
├── settings.py
└── urls.py


---