# Function for MVP

- [ ]  Mission for turn off alarm
- [ ]  Ringtone
- [ ]  Vacation mode
- [ ]  Use iOS 26 **AlarmKit framework** for better alarm
- [ ]  Wake up check - 20 sec then go off again
- [ ]  7.99$ for life time
- [ ]  multiple mission at once
- [ ]  preventing snooze ( wake up check)

---

- Question need to be defined
    
    ● High‑impact areas to clarify or detail
    
    Here are the most important ambiguities and decision points to lock
    down. For each, I include crisp questions and a reasonable default if
    you want me to apply one now.
    Wake‑Up Check timing and behavior
    • Interaction definition: What counts as “interaction”? Only in‑app
    touches, or also notification taps, unlock, volume/power buttons?
    
        • Default: Count in‑app tap/gesture OR tapping the “I’m awake”
          notification action.
     • Window lifecycle: After the 3rd window elapses with no
       interaction, does the alarm keep cycling, escalate, or stop?
        • Default: Cycle once more using the last window length, then
          stop and mark “Wake‑up check failed”.
     • Vacation mode interplay: If vacation mode is ON and alarm is
       dismissed without missions, do wake‑up checks still run?
        • Default: No wake‑up checks when vacation mode is ON.
     • Foreground/background constraints: If the app is backgrounded,
       how is interaction captured and how accurate must timers be?
        • Default: Timers may have ±5s tolerance in background;
          notification action counts as interaction.
    
    Snooze policy
    • Snooze on mission alarms: If missions exist, can the user snooze
    before completing missions?
    • Default: Yes, snooze allowed unless disabled; missions still
    required when alarm re‑rings.
    • Limits: Max snooze count per alarm ring? Allowed intervals (e.g.,
    5/10/15 min or free entry)?
    • Default: Up to 3 snoozes; intervals 5/10/15 min.
    
    Vacation mode scope
    • Time‑bounded? Is vacation mode a toggle or time‑range (e.g.,
    until next weekday)?
    • Default: Per‑alarm toggle that persists until manually turned
    off.
    • Visual safety: Require confirmation when enabling during an active
    ring?
    • Default: Yes, confirm to avoid accidental bypass.
    
    Mission orchestration (multiple missions per alarm)
    • Order and UX: Complete missions in any order or predefined
    sequence?
    • Default: Any order; all must be completed.
    • Timeouts and retries: Does a mission have a time limit before
    re‑ring triggers?
    • Default: No hard mission timeouts; re‑ring governed by wake‑up
    check windows only.
    • Failure handling: Can user switch mission type mid‑ring if, e.g.,
    camera permission denied?
    • Default: Allow switching only if configured as an alternate
    beforehand; otherwise re‑ring.
    Barcode/QR mission specifics
    • Registration source: User scans a code at setup; do we allow
    uploading an image or generating a code?
    • Default: Scan at setup only; no image upload/generation.
    • Matching criteria: Exact content match only? Orientation/format
    normalization?
    • Default: Exact payload match; whitespace/encoding normalized.
    • Offline behavior: Must scanning work offline?
    • Default: Yes, match local payload.
    
    Typing mission specifics
    • Matching rules: Case sensitivity, punctuation, whitespace, emoji,
    non‑Latin scripts?
    • Default: Exact Unicode string match, including case and
    punctuation; leading/trailing whitespace normalized.
    • Anti‑cheat: Allow copy/paste?
    • Default: Disallow paste on the input field.
    • Language: Paragraph language selection?
    • Default: Follows device locale; English fallback.
    
    Math mission specifics
    • Operations per level: Which operators at each of the 5 levels?
    Integers only? Negative numbers? Division remainder?
    • Default:
    • L1: +/−, 1–20
    • L2: +/−/×, 1–50
    • L3: +/−/×/÷ (integer division), 1–100, no negatives
    • L4: +/−/×/÷ with parentheses, 1–200, negatives allowed
    • L5: Multi‑step expressions (3–5 ops), 1–500, negatives
    allowed
    • Attempts: Limited attempts or unlimited until correct?
    • Default: Unlimited attempts; re‑ring windows still apply.
    Alarm sound and start signals
    • Sound behavior: Fade‑in, min/max volume, respect silent/DND?
    • Default: Respect system volume/DND; optional 3s fade‑in;
    fallback to notification when sound suppressed.
    • Preview constraints: Preview volume and duration?
    • Default: Preview ≤5s at current volume.
    
    Scheduling and recurrence (not yet specified)
    • Repeat rules: Weekdays/weekends/custom? Time‑zone and DST
    handling?
    • Default proposal: Standard recurrence (daily/weekly/custom
    days), TZ‑aware; DST “same local time” rule.
    Concurrency and conflicts
    • Overlapping alarms: UI/priority when two alarms ring; do both
    play?
    • Default: New ring queues behind active ring with a banner to
    switch; both never play simultaneously.
    Accessibility and localization
    • Screen reader prompts for missions; haptics for signals;
    color‑contrast for typing mission.
    • Default: Provide VoiceOver/TalkBack labels, haptic cues, and
    WCAG‑conformant contrast.
    
    Privacy, security, and data
    • Storage of mission data (QR payloads, paragraphs) and encryption;
    analytics/telemetry scope.
    • Default: Store locally; encrypt at rest if platform supports;
    minimal anonymous telemetry with opt‑out.
    • Anti‑bypass: Prevent screenshots or cached text revealing
    answers?
    • Default: Do not display math answers; typing paragraphs
    generated per ring and not copied.
    Observability and versioning (from constitution)
    • Logging: What events are logged? (ring, dismiss, snooze, mission
    success/failure, wake‑up check events)
    • Default: Log these events in structured form with timestamps.
    • Breaking changes: Policy if mission logic changes (e.g., level
    definitions).
    • Default: SemVer MINOR for additive; MAJOR for changes to
    mission completion semantics.
    
    Top 5 decisions to make now (to unblock planning)
    1. Wake‑Up Check end‑of‑sequence behavior after 3 windows (stop vs
    continue cycling).
    2. Whether vacation mode disables wake‑up checks entirely.
    3. Snooze policy on mission alarms (allowed? max snoozes?
    intervals).
    4. Typing mission matching rules (case/whitespace/paste).
    5. Math mission operator set per level and integer vs decimal
    policy.