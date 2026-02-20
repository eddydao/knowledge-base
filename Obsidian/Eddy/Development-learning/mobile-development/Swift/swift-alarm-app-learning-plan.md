# Swift_Alarm_App_LearningPlan

# Swift + iOS Alarm App Learning Plan (Beginner → Complete App)

**Time commitment:** ~2 hours/day

**Outcome:** Learn core Swift & SwiftUI and ship a fully working **Alarm app** (multi-alarm CRUD, local notifications, custom sounds, snooze, and 3 missions: **Barcode/QR**, **Typing**, **Math**) with privacy and persistence.

---

## 📌 How to Use This Plan

- Each day starts with **theory** then **practice** that directly adds to your app.
- Each **Practice** clearly states where to work:
💡 *(in Playground)* — quick Swift coding and experiments.
🧱 *(in Xcode App project)* — building real app features.
- If you miss a day, pick up from where you left off; all sessions are incremental.
- Keep Xcode open with your project and a **Swift Playground** for quick tests.

---

## Week 1 — Swift Basics & SwiftUI Foundations

### Day 1 — Swift & Environment Setup

**Theory:** Xcode, Playgrounds, `let` vs `var`, basic types (Int, String, Bool), `print`, string interpolation.

**Practice (in Playground):**
- Create a Playground; print `Hello, World!` and `"You have \(currentAlarms) alarms"`.
- Try: `let maxAlarms = 50`, `var currentAlarms = 0`; mutate `currentAlarms`.
- (Notes) Decide project name: **WakeMe**.

---

### Day 2 — Types, Control Flow, Collections

**Theory:** Arrays, Dictionaries, `if/else`, `switch`, `for` loops.

**Practice (in Playground):**
- Array: `let times = [6, 6, 30, 7, 0]` (represent 06:30, 07:00, etc.). Loop & print.
- Dictionary: `["Mon": true, "Tue": false]`; loop & state which days have alarms.
- Practice `switch` with ranges for scoring.

---

### Day 3 — Functions & Optionals

**Theory:** Functions, params/return, Optionals, `if let` / `guard let`, `??`.

**Practice (in Playground):**
- `func formatAlarmLabel(hour: Int, minute: Int) -> String` → `"06:30"`.
- `var alarmNote: String?`; unwrap safely; default with `?? "Alarm"`.

---

### Day 4 — Structs vs Classes; App Models

**Theory:** Value vs reference types; initializers; methods; computed properties.

**Practice (in Playground):**
- `struct Alarm { var time: Date; var label: String; var isEnabled: Bool }`.
- Copy semantics demo (struct) vs shared semantics (class `AlarmManager`).

---

### Day 5 — Enums & App Planning

**Theory:** `enum Weekday`, `enum MissionType { case barcode, typing, math }`.

**Practice (in Playground):**
- `Weekday` with `isWeekend` computed property.
- Write a one-page feature outline for your app (alarms, sounds, snooze, missions, persistence, notifications).

---

### Day 6 — SwiftUI Views & Layout

**Theory:** SwiftUI `View`, `body`, `VStack/HStack`, modifiers, Preview.

**Practice (in Xcode App project):**
- Create your first **SwiftUI App** project named **WakeMe** in Xcode.
- Replace `ContentView` with `Text("Hello, SwiftUI Alarm!")` + `.font(.headline).padding()`.
- Add a `Button("Tap Me") { print("Tapped") }` inside a `VStack`.

---

### Day 7 — SwiftUI State

**Theory:** `@State`, reactive updates, data flow.

**Practice (in Xcode App project):**
- `@State private var alarmCount = 0`; Button increments; Text shows value.
- Add `Toggle("Alarm Enabled", isOn: $enabled)` in a small `AlarmRow` view.

---

## Week 2 — Core App: List, Detail, Persistence, Notifications

### Day 8 — Alarm List UI & Navigation

**Theory:** `List`, `NavigationStack`, `NavigationLink`.

**Practice (in Xcode App project):**
- `AlarmListView`: `List` of placeholder alarms, `.navigationTitle("My Alarms")`.
- Toolbar `+` button → `AlarmDetailView` via `NavigationLink` or `.sheet`.

---

### Day 9 — Alarm Detail Form

**Theory:** `Form`, `DatePicker(.hourAndMinute)`, `TextField`, `Toggle`.

**Practice (in Xcode App project):**
- Build `AlarmDetailView` with fields: time, label, snooze toggle.
- Add Save button (for now, prints values or passes back via binding).

---

### Day 10 — ObservableObject ViewModel

**Theory:** `ObservableObject`, `@Published`, `@StateObject`, `.environmentObject`.

**Practice (in Xcode App project):**
- `final class AlarmData: ObservableObject { @Published var alarms: [Alarm] = [] }`.
- Use `@StateObject var alarmData = AlarmData()` in parent view.
- Save from Detail → append to `alarmData.alarms` → List updates automatically.

---

### Day 11 — Core Data Setup

**Theory:** Core Data model, `NSPersistentContainer`, managed object context.

**Practice (in Xcode App project):**
- Add Data Model: **Alarm** entity (time: Date, label: String, isEnabled: Bool, snoozeEnabled: Bool).
- Ensure Core Data stack is created (template or manual). Provide `moc` via environment.

---

### Day 12 — Persist Alarms

**Theory:** `@FetchRequest`, `NSManagedObject`, CRUD.

**Practice (in Xcode App project):**
- `@FetchRequest(sortDescriptors: []) var savedAlarms` in list view.
- On Save: create `AlarmEntity`, set fields, `try? moc.save()`.
- Swipe-to-delete: `onDelete` → `moc.delete` + save.
- Relaunch app: alarms persist.

---

### Day 13 — Protocols, Extensions, Logging

**Theory:** Protocols (blueprints), extensions (add behavior), basic logging.

**Practice (in Xcode App project):**
- `protocol AlarmMission { var type: MissionType { get } }` (for missions).
- Extension: `AlarmEntity.displayTime: String` (format `Date`).
- Add simple logger using `os.Logger` and ensure no PII is logged.

---

### Day 14 — Local Notifications (Ring)

**Theory:** `UNUserNotificationCenter`, permissions, `UNCalendarNotificationTrigger`.

**Practice (in Xcode App project):**
- Request authorization `.alert, .sound`.
- On Save: schedule notification for alarm time with `UNNotificationRequest`.
- Test in simulator or real device to verify ring while app is in background.

---

## Week 3 — Missions: Barcode/QR, Typing, Math

### Day 15 — Mission Modeling & Selection

**Theory:** One-to-many (Alarm ↔︎ Missions). Simple per-alarm mission selection.

**Practice (in Xcode App project):**
- In Detail, add Picker: mission type (None/Barcode/Typing/Math).
- Store selection in Core Data or memory.
- Plan flow: ring → present mission → Dismiss enabled after mission complete.

---

### Day 16 — Barcode/QR Registration (Camera)

**Theory:** VisionKit `DataScannerViewController` or AVFoundation; camera privacy.

**Practice (in Xcode App project):**
- Add `NSCameraUsageDescription` to Info.plist.
- Create `BarcodeScannerView` (UIKit wrapped via `UIViewControllerRepresentable`).
- In Detail (when mission type == .barcode): button **Register Code** → scan → save barcode value.

---

### Day 17 — Barcode Dismissal Flow

**Theory:** Ring-time mission enforcement; match scanned code.

**Practice (in Xcode App project):**
- `AlarmRingView`: if `.barcode`, show scanner; compare scanned vs stored.
- Disable “Dismiss” until match succeeds.
- Test both correct/incorrect scenarios.

---

### Day 18 — Typing Mission: Corpus & Difficulty

**Theory:** Resource loading, difficulty tiers, random selection.

**Practice (in Xcode App project):**
- Add `typing_texts_en.txt` to bundle.
- `func randomText(for difficulty)` → choose text length by level.
- Add difficulty Picker in Detail view.

---

### Day 19 — Typing Mission: UI & Validation

**Theory:** `TextEditor`, validation logic, text matching.

**Practice (in Xcode App project):**
- Create `TypingMissionView(target: String)`.
- Show text target, TextEditor input, and “Submit” button.
- Compare input == target; show success before enabling Dismiss.

---

### Day 20 — Math Mission: Problem Generator

**Theory:** Random math generation, level-based difficulty.

**Practice (in Xcode App project):**
- Define levels (1–5); generate random problems.
- Create struct `MathProblem { var question: String; var answer: Int }`.
- Build generator: `generateProblem(level:) -> MathProblem`.

---

### Day 21 — Math Mission: UI, Timer, Completion

**Theory:** SwiftUI timers, state management, progress tracking.

**Practice (in Xcode App project):**
- Create `MathMissionView(level:)`.
- Show question + numeric input + countdown timer.
- Correct → increment; finish after N correct answers → unlock Dismiss.

---

## Week 4 — Polish: Sound, Snooze, Privacy, QA

### Day 22 — Sound Selection & Snooze

**Theory:** AVAudioPlayer preview, notification sound linking, snooze logic.

**Practice (in Xcode App project):**
- Add sound picker to Detail view with preview (AVAudioPlayer).
- Save selected sound to Core Data.
- Use `UNNotificationSound(named:)` or local playback.
- Snooze button reschedules notification (+X min) unless missions exist.

---

### Day 23 — Privacy & Security

**Theory:** Permissions, Keychain, secure storage, data protection.

**Practice (in Xcode App project):**
- Confirm Info.plist permissions.
- Ensure Core Data store protection (CompleteUntilFirstUserAuthentication).
- Encrypt mission payloads using CryptoKit AES-GCM.
- Store keys in Keychain (ThisDeviceOnly).

---

### Day 24 — Accessibility & QA

**Theory:** Accessibility modifiers, color contrast, dynamic type.

**Practice (in Xcode App project):**
- Add `.accessibilityLabel` to all interactive elements.
- Test all missions + alarm flow manually.
- Optional: Add lightweight event logger for QA (no sensitive data).

---

## ✅ Final Deliverable

- Multi-alarm CRUD (list/detail, enable/disable, delete).
- Local notifications ring at time; custom sounds.
- Snooze (disabled when missions active).
- Missions: **Barcode/QR**, **Typing**, **Math** implemented and enforced.
- Data persisted in **Core Data**; privacy-first (no PII in logs, secure at rest).
- Accessibility compliance and QA verified.

---

## ✍️ Daily Checklist (Copy/Paste)

- [ ]  Theory finished (watch/read/skim notes)
- [ ]  Exercises completed
- [ ]  Code committed
- [ ]  Next-day prep done

---

## 📂 Suggested Project Structure (high level)

```
ios/WakeMeApp/
  App.swift
  Resources/
    typing_texts_en.txt
    sounds/
  Features/
    AlarmList/
    AlarmDetail/
    AlarmRing/
    Missions/
      Barcode/
      Typing/
      Math/
Persistence/
  CoreData model + stack
Shared/
  Models/
  ViewModels/
  Utilities/ (Logger, Formatters)
```