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


PauseSend (MVP)

I built PauseSend because the architecture of modern communication is fundamentally biased toward speed over intent. Most messaging platforms are designed to reduce friction, but in doing so, they’ve eliminated the space for reflection. We send things before we've fully processed them, and once a message hits the server, the social cost is already paid.

This project is a custom Android Keyboard (IME) that functions as a mechanical buffer. It creates a deliberate gap between the thought and the transmission.
The Problem

Instant messaging creates a false sense of urgency. The "Send" button has become a reflex rather than a choice. We’ve all felt that immediate hit of regret the second a message leaves the device—what I call "the split-second correction." Existing solutions, like "Delete for Everyone," are reactive and leave a digital scar. PauseSend is proactive; it keeps the message on your device until you’re certain.
The Solution

The app functions as a system-level interceptor. Instead of the keyboard immediately committing text to the target application (like WhatsApp or Slack), it holds it in a temporary state.

    Interception: The keyboard catches the "Send" action at the system layer.

    Buffer: Text is stored in a volatile local buffer.

    Countdown: A visual timer triggers, creating a window of 3 to 10 seconds.

    Agency: During this window, you have the physical opportunity to retract the message or refine the language before the OS ever sees the data.

Technical Choices

The stack was chosen to prioritize system stability and low-level control:

    Kotlin and Coroutines: I used Coroutines to manage the delay engine. This was a necessity—handling a countdown on the main thread would freeze the keyboard, making it unusable. Coroutines allow the timer to run in the background while keeping the UI responsive.

    InputMethodService API: This is the heart of the project. Building a keyboard is different from building a standard app; it’s a persistent service that must be trusted by the operating system. It required a deep dive into how Android manages the bridge between the user’s input and the app’s text field.

    Jetpack Compose: I used Compose to build the overlay and settings. It allowed for a more declarative way to handle the "countdown" state without the overhead of traditional Android views.

    DataStore: To keep things lightweight, I used DataStore for persistence. It ensures that your preferred delay settings are loaded asynchronously, preventing any "jank" during keyboard startup.

Privacy and Integrity

Keyboards are a massive privacy risk, so I built this with a zero-trust approach toward the cloud.

    Local-Only: There is no networking logic. The app cannot send data to an external server because it doesn't have the permission to do so.

    Volatile Storage: Messages are held in memory only for the duration of the timer. Once the message is sent or cancelled, the buffer is purged.

Reflection

The biggest challenge wasn't the UI—it was the InputConnection logic. Every app handles "committing" text differently. Ensuring that the pause felt like a natural extension of the OS, rather than a glitch in the interface, required significant tuning of the service lifecycle.

Author
Mogau Mapodile
Software Engineering Student
Focusing on Platform Engineering and building tools that bridge the gap between human psychology and technical infrastructure.