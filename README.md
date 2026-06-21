# Polly - On-Device AI Chat (Apple Intelligence)

> A conversational chat with **Rob8**, an eco-conscious robot companion, running **100% on-device**
> with Apple's **FoundationModels** framework (Apple Intelligence). No network, no server, **no API key**.

Part of **Polly**, a gamified iOS app that helps users cut their **digital carbon footprint**
(screen time, data storage, digital habits). Built at the **Apple Developer Academy**.

---

## What it demonstrates

| Area | Skill shown |
|------|-------------|
| **On-device LLM** | `FoundationModels`: `LanguageModelSession`, `session.respond(to:)` - runs offline on the Neural Engine |
| **Prompt engineering** | Defining a persona/tone/scope with `Instructions(...)` (the system prompt) |
| **Conversation context** | The session keeps multi-turn context automatically |
| **Async Swift** | `async/await` calls, `@MainActor` view model |
| **MVVM** | `ChatViewModel: ObservableObject` driving the UI with `@Published` state |
| **SwiftUI chat UI** | Message bubbles, animated typing indicator, auto-scroll, send-on-submit |

---

## The core: an offline language model session

The whole AI integration is just a few lines - no SDK, no keys, no networking:

```swift
import FoundationModels

// 1. Define the assistant's persona (system prompt)
let instructions = Instructions("""
    You are Rob8, an eco-conscious digital robot companion inside the Polly app.
    You speak in short, punchy messages and give practical eco-digital tips.
    """)

// 2. Open an on-device session (keeps conversation context)
let session = LanguageModelSession(instructions: instructions)

// 3. Send a message and await the model's reply - fully on-device
let response = try await session.respond(to: userText)
messages.append(.init(role: "assistant", text: response.content))
```

Because the model ships with Apple Intelligence and runs locally, the chat works **in airplane mode**
and never sends the user's words off the device - a real privacy and sustainability win.

---

## What's in this repo

A **portfolio excerpt** - the AI/chat layer only:

- [`Rob8Chat.swift`](Rob8Chat.swift) - `ChatViewModel` (FoundationModels integration) + the SwiftUI chat UI (`ChatView`, message bubbles, typing indicator).

The rest of the app (gamification/`GameManager`, home, podcasts, onboarding) is intentionally omitted.

---

*Built with Swift, SwiftUI, FoundationModels (Apple Intelligence) - Apple Developer Academy project.*
