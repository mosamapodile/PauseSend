# PauseSend
# project structure 

PauseSend/
├── app/
│   ├── src/main/
│   │   ├── java/com/pausesend/
│   │   │   ├── ime/                 # The Heart: Custom Keyboard Service
│   │   │   │   ├── PauseSendIME.kt  # Inherits InputMethodService
│   │   │   │   └── KeyboardView.kt  # Compose-based keyboard UI
│   │   │   ├── logic/               # The Delay Engine
│   │   │   │   └── SendManager.kt   # Coroutine-based timer & buffer
│   │   │   ├── ui/                  # Settings & Onboarding
│   │   │   │   ├── SettingsActivity.kt
│   │   │   │   └── SettingsViewModel.kt
│   │   │   └── data/                # Local Config
│   │   │       └── Preferences.kt   # DataStore for delay settings
│   │   ├── res/                     # Layouts, XML, and Icons
│   │   │   └── xml/
│   │   │       └── method.xml       # Crucial: Registers IME with Android
│   │   └── AndroidManifest.xml      # Declares the Service & Permissions
├── build.gradle.kts                 # Project Dependencies
└── README.md                        # Documentation


# PauseSend (MVP) 🧠⌨️

**PauseSend** is a specialized Android Input Method Editor (IME) designed to act as a "buffer between emotion and communication." It introduces an intentional, configurable delay before messages are committed to the host application, allowing users to edit or retract impulsive texts.

## 🚀 The Problem
"Sender's Remorse" happens in seconds. Most communication apps send messages instantly, leaving no room for a second thought.

## 🛠️ The Solution (MVP)
PauseSend intercepts the "Send" action at the system level, holds the text in a local buffer, and displays a countdown. 
- **Retract:** Cancel the send before the timer hits zero.
- **Refine:** Edit the text while it’s in the buffer.
- **Commit:** Automatic send after the delay expires.

## 🏗️ Tech Stack
- **Language:** [Kotlin](https://kotlinlang.org/) (Coroutines for non-blocking delay logic)
- **Framework:** [Android SDK](https://developer.android.com/) (InputMethodService)
- **UI:** [Jetpack Compose](https://developer.android.com/jetpack/compose) (Reactive UI for the keyboard and settings)
- **Architecture:** MVVM (Model-View-ViewModel)
- **Local Storage:** Jetpack DataStore (Configuration management)

## 📋 Core Features
- [ ] **Custom IME Service:** A functional system keyboard that can be enabled in Android Settings.
- [ ] **The Delay Engine:** A 3–10 second configurable countdown using Kotlin Coroutines.
- [ ] **Preview Overlay:** A real-time UI element showing the pending message and a 'Cancel' button.
- [ ] **Settings Dashboard:** Toggle PauseSend on/off and adjust delay sensitivity.

## 📂 Project Structure
- `ime/`: Contains `InputMethodService` implementation for system-level text interception.
- `logic/`: Management of the message buffer and coroutine-based timers.
- `ui/`: Compose-based views for the keyboard layout and the settings activity.
- `data/`: Persistence layer for user-defined delay intervals.

## 🛡️ Privacy & Security
PauseSend is built with privacy-first principles. 
- **Local Processing:** All text buffering happens strictly on-device. 
- **Zero Logging:** No keystrokes or message contents are stored permanently or transmitted to external servers.

## 👨‍💻 Author
**Mogau Mapodile**  
*Software Engineering Student | Aspiring Platform Engineer*