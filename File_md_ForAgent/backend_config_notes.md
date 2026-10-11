# Backend Configuration & Notes (Web & API)

This file tracks technical requirements, API structures, and configuration details that will be needed when building the Website and Backend for the application.

## 1. Audio & Reciters API
- **Primary Source**: `mp3quran.net/api/v3`
- **Data Structure Needed**:
  - We need a unified JSON endpoint on our backend that serves the reciters list so we can update it without releasing a new app update.
  - Required fields per reciter: `id`, `name`, `rewaya`, `server_url`, `image_url`.
- **Images**:
  - Currently, images are stored locally in the app (`assets/images/reciters/`). 
  - *Action for Web*: Create an AWS S3 bucket (or similar CDN) to host high-quality, uniformly cropped photos of reciters. The backend API should return the CDN URL.

## 2. Audio Timing Engine (Ayah-by-Ayah)
- **Source**: `https://mp3quran.net/api/v3/ayat_timing?surah={surah}&read={read_id}`
- **Note for Web**: The web platform should mimic the mobile app's architecture. Do NOT fetch Ayah-by-Ayah MP3s. Instead, fetch the full Surah MP3 and use the timing JSON to `seek()` and highlight the SVGs on the web.

## 3. Downloads & Offline Storage
- The mobile app saves files to `ApplicationDocumentsDirectory`.
- Files saved: `<Reciter_ID>_surah_<Surah_Number>.mp3`.
- *Action for Backend*: If we introduce user accounts, we should sync the user's "Downloaded/Favorite Surahs" library to their profile.

## 4. Playback Settings
- We need to persist user preferences (e.g., Default Reciter, Sleep Timer settings, Repeat settings).
- *Schema Suggestion*:
  ```json
  {
    "user_id": "123",
    "preferences": {
      "default_riwaya": "hafs",
      "default_reciter_id": 102,
      "sleep_timer_default_minutes": 30
    }
  }
  ```

## 5. Lesson Sources (المصادر) - Fiqh / Learn
- **Requirement**: We added a UI in `LessonResultScreen` to display additional references and sources at the end of a lesson.
- **Action for Backend**: When sending the node content in `GET /paths/:pathId/nodes/:nodeId`, please ensure you include a `sources` array (or include it in the `complete` node response). 
- **Expected Schema**:
  ```json
  "sources": [
    {
      "book": "فتح القريب المجيب في شرح ألفاظ التقريب",
      "link": "https://shamela.ws/book/9780"
    }
  ]
  ```
  *(The mobile app specifically looks for the `link` and `book` keys. If this is missing or named differently, the sources will simply not appear in the result screen).*
