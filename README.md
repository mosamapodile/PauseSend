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