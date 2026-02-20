# Two_Week_Swift_Notion_Format

# 🚀 Two-Week Swift Learning & Building Plan

Goal: Build a small but functional iOS app (for example, a “Meal Planner” MVP) using SwiftUI, Firebase Auth, and simple API connections.

---

## 🗓️ Week 1 — Learn Just Enough Swift + SwiftUI to Build UI

### 🎯 Objective

Understand Swift syntax, build screens in SwiftUI, and manage simple state.

**Day 1–2: Swift Crash Course**

- [ ]  Learn variables, constants, and data types (String, Int, Bool)
- [ ]  Understand functions and optionals (? , guard let)
- [ ]  Learn difference between Structs and Classes
- [ ]  Practice using Array and Dictionary
- [ ]  Practice: Build a small console “calculator” or “todo list” app in Playground

**Day 3–4: SwiftUI Fundamentals**

- [ ]  Use SwiftUI views: Text, Image, Button, List, VStack, HStack
- [ ]  Add navigation with NavigationStack and NavigationLink
- [ ]  Manage state with @State and @Binding
- [ ]  Create multiple screens with navigation
- [ ]  Practice: Build a 2-screen “Daily Habits” or “Meals” app

**Day 5–6: State and Data Flow**

- [ ]  Learn about @ObservedObject, @StateObject, and EnvironmentObject
- [ ]  Apply MVVM pattern (Model–View–ViewModel)
- [ ]  Use mock JSON data and dynamic list rendering
- [ ]  Practice: Display a list of meals or dishes from mock data

**Day 7: Backend Intro**

- [ ]  Learn URLSession for REST API requests
- [ ]  Parse JSON using Codable
- [ ]  Display data from API in SwiftUI
- [ ]  Practice: Connect to your /api/menus/get-suggestion endpoint

---

## 🗓️ Week 2 — Add Firebase + Deploy an MVP

### 🎯 Objective

Add authentication, persistence, and ship a working MVP.

**Day 8–9: Firebase Auth and Firestore**

- [ ]  Add Firebase SDK to your Xcode project
- [ ]  Implement Google Sign-In or Email/Password login
- [ ]  Create Firestore collections (e.g. user preferences, favorites)
- [ ]  Practice: Save user’s favorite meal IDs to Firestore

**Day 10–11: Integrate Your Backend API**

- [ ]  Fetch meal suggestions for the logged-in user
- [ ]  Handle loading and error states
- [ ]  Bind backend data to SwiftUI list or grid
- [ ]  Practice: Build a “Meal Dashboard” fetching live data

**Day 12–13: UI Polish and Notifications**

- [ ]  Add icons using SF Symbols and improve colors
- [ ]  Set up Firebase Cloud Messaging or local notifications
- [ ]  Test app flow on real device
- [ ]  Practice: Notify user daily about new meal suggestions

**Day 14: Wrap Up**

- [ ]  Debug and finalize onboarding and meal suggestion flow
- [ ]  Build for release (TestFlight)
- [ ]  Reflect and document improvements for version 2

---

## ✅ Final Deliverable

A working iOS app where users can:
- Log in with Google or Apple
- View meal suggestions from your backend
- Save favorites to Firestore
- Receive a daily notification reminder
- Run the app on an actual iPhone or via TestFlight