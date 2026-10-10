# Aura Co-Pilot 🤖📱

An advanced, offline-first Android voice assistant built for the **Nothing Phone (2a)** using **Kotlin**, **Jetpack Compose**, **Picovoice Porcupine** (wake-word detection), and **Gemini API** integration. Designed to provide hands-free system automation, accessibility-driven form filling, and secure document retrieval.

## 🌟 Key Modules & Architecture

### 1. Speech & Intent Processing (`speech/`)
* **`WakeWordManager`**: Listens continuously for local wake-word triggers ("Aura") using low-latency on-device processing.
* **`SpeechManager`**: Handles speech-to-text transcription and text-to-speech audio feedback.
* **`IntentRouter`**: Parses transcribed commands using keyword matching (`lowerCommand.contains()`) to route tasks dynamically to the appropriate controller (WhatsApp, Calls, Vault, Vision, Form Filling).

### 2. Form Auto-Filler & Accessibility (`form/` & `service/`)
* **`FormAutoFiller`**: Traverses the active window node hierarchy (`AccessibilityNodeInfo`) to locate input fields matching specific keywords (*name, dob, aadhaar, phone, address*).
* **`AuraAccessibilityService`**: A background accessibility service that injects secure user data directly into form text fields on screen via `ACTION_SET_TEXT`.

### 3. Secure Vault / DigiLocker Integration (`digilocker/`)
* **`SecureVault`**: Utilizes Android's `EncryptedSharedPreferences` backed by `MasterKey` (AES256-GCM encryption) to securely store and load sensitive user identity details locally without cloud exposure.

### 4. Communication & Control (`call/`)
* **`CallController`**: Interacts with Android's `ContactsContract` to perform fuzzy name lookups (e.g., "Call Mom") and initiates secure phone calls (`Intent.ACTION_CALL`).

### 5. Vision Engine (`vision/`)
* **`SpatialVisionEngine` & `CameraFrameCapture`**: Captures camera frames for environmental description and spatial analysis.

## 🛠️ Tech Stack & Requirements
* **Language**: Kotlin
* **UI**: Jetpack Compose, Material 3
* **Min SDK**: Android 14+ (Targeted for Android 16, API 35+)
* **Permissions Required**: `RECORD_AUDIO`, `READ_CONTACTS`, `CALL_PHONE`, `BIND_ACCESSIBILITY_SERVICE`
