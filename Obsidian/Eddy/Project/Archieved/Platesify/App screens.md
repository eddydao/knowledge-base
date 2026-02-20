**Core Philosophy (based on reference):**
*   **Visually Driven:** High-quality food imagery is key.
*   **Simple & Clean:** Uncluttered interface, easy to navigate.
*   **Encouraging:** Positive language ("Cook Special Every Day," "Let's Making" - though we'll correct the grammar).
*   **Informative at a Glance:** Key details like time, difficulty, and rating are prominent.

---

**I. Visual Design Language (Derived from Reference):**

*   **Color Palette:**
    *   **Primary Background:** White / Very Light Grey (as seen)
    *   **Accent Color (Primary):** Vibrant Green (for CTAs, highlights, active states - e.g., #65B95C from "Let's Making" button)
    *   **Accent Color (Secondary):** A softer, perhaps desaturated green or a complementary warm color for tags or secondary info.
    *   **Text Colors:** Dark Grey/Black for primary text, Medium Grey for secondary text.
    *   **Icon Colors:** Medium Grey, Green for active/selected icons.
*   **Typography:**
    *   **Headings:** A clean, modern sans-serif font (similar to Montserrat, Lato, or Proxima Nova). Bold for main titles.
    *   **Body Text:** Regular weight of the same sans-serif font family for readability.
*   **Iconography:** Simple, clean, slightly rounded line icons or filled icons (as seen in the bottom bar and category selectors).
*   **Imagery:** High-quality, appetizing photos of food are crucial.
*   **Card Style:** Rounded corners, subtle drop shadows for depth (as seen on the Miso Ramen card and ingredient items).
*   **Buttons:** Rounded corners. Primary CTAs are filled with the accent green. Secondary buttons could be outlined or use a lighter shade.
*   **Layout:** Generous use of whitespace. Clear visual hierarchy.

---

**II. Key Screens & Features:**

**1. Splash Screen & Onboarding (New)**
    *   **Splash:** App logo (e.g., a stylized chef's hat or a fork/knife icon) with the app name "Daily Dish" on a plain background.
    *   **Onboarding (Optional but Recommended):**
        *   Few screens highlighting key features (e.g., "Discover daily recipes," "Filter by your preferences," "Save your favorites").
        *   Option to set initial dietary preferences (e.g., vegetarian, gluten-free, allergies) or cuisine preferences.
        *   Sign Up / Log In / Skip for now.

**2. Home Screen (Based on Reference - Screen 1)**
    *   **User Profile Snippet:** (Top Left) User avatar, Name ("Juliana Silva"), Status ("Basic" - could imply premium features later).
    *   **Notifications:** (Top Right) Bell icon.
    *   **Main Greeting:** "Cook Special Every Day" (or dynamic greeting like "What to cook today, Juliana?").
    *   **Search Bar (Enhancement):** Prominently placed below the greeting. "Search recipes, ingredients..."
    *   **Categories:** (Horizontal scroll or wrap) "Appetizers," "Soups & Stews," "Main Courses," "Desserts," "Breakfast," "Quick Meals," "Vegetarian," etc. Each with a small illustrative icon.
    *   **Featured/Recommended Section:**
        *   "Today's Special" or "Recommended for You" (large card like "Miso Ramen").
        *   Could also have "Trending Recipes," "Seasonal Dishes," or "Quick & Easy."
        *   Recipe cards show: Image, Title, Key Info (e.g., cooking time, rating), Save/Favorite icon.
    *   **Bottom Navigation Bar:**
        *   **Home:** (Active)
        *   **Search/Discover:** (Magnifying glass icon) - Could lead to a more advanced search/filter page.
        *   **Favorites:** (Heart icon)
        *   **Profile/Settings:** (User icon)

**3. Recipe Detail Screen (Based on Reference - Screen 2)**
    *   **Navigation:** Back arrow (top left), Favorite/Save icon (top right - heart).
    *   **Recipe Image:** Large, high-quality.
    *   **Category Tag:** "Soups & Stews" (or relevant category).
    *   **Recipe Title:** "Miso Ramen."
    *   **Quick Info Bar:**
        *   Cooking Time (e.g., "20m Minutes")
        *   Number of Steps (e.g., "10 Steps") or Servings
        *   Difficulty (e.g., "Easy")
        *   Rating (e.g., "5.0 Rating") - Tappable to see reviews.
    *   **Tabs (Enhancement):**
        *   **Ingredients:** (Selected by default)
            *   List of ingredients with small icon/image, name, quantity (e.g., "Egg - 2x pcs," "Chicken meat - 1/4 kg").
            *   Option to "Add to Shopping List."
        *   **Instructions:**
            *   Numbered steps. Clear, concise instructions.
            *   Option for a "Cooking Mode" (see below).
        *   **Nutrition (Optional):** Basic nutritional info (calories, protein, carbs, fats).
        *   **Reviews (Optional):** User reviews and ratings.
    *   **Primary CTA:** "Start Cooking" (corrected from "Let's Making") - Large green button.

**4. Cooking Mode Screen (New - Accessed from Recipe Detail)**
    *   **Distraction-Free Interface:** Focuses on one step at a time.
    *   **Step Display:** "Step 1 of 10" - Large, easily readable text for the current instruction.
    *   **Navigation:** "Previous Step," "Next Step" buttons. Swipe gesture support.
    *   **Ingredients for Current Step (Optional):** List relevant ingredients for the active step.
    *   **Timers:** If a step involves timing (e.g., "Simmer for 10 minutes"), an integrated timer can be started.
    *   **Check-off:** Ability to mark steps as complete.
    *   **Keep Screen Awake:** Option to prevent the screen from locking.
    *   **Exit Cooking Mode:** Clear button to return to Recipe Detail.

**5. Favorites Screen (New - Accessed from Bottom Nav)**
    *   **Title:** "My Favorite Recipes."
    *   **Layout:** List or grid of saved recipe cards.
    *   **Functionality:** Tap to view recipe, option to remove from favorites.
    *   **Empty State:** Message like "You haven't saved any recipes yet. Explore and find your favorites!" with a button to "Discover Recipes."

**6. User Profile Screen (New - Accessed from Bottom Nav)**
    *   **User Avatar & Name.**
    *   **Account Status:** "Basic" or "Premium."
    *   **Sections:**
        *   **My Dietary Preferences:** Manage allergies, liked/disliked cuisines, etc.
        *   **Shopping Lists (If implemented):** Access saved shopping lists.
        *   **My Meal Plan (Future enhancement):** If a meal planning feature is added.
        *   **Settings:**
            *   Notifications (new recipes, cooking reminders).
            *   Account (change password, email).
            *   Subscription (if premium features exist).
            *   About Us, Help & Support, Privacy Policy.
        *   **Log Out.**

---

**III. User Flow Examples:**

*   **Finding and Cooking a Recipe:**
    1.  Open App -> Home Screen
    2.  Browse Categories or Featured -> Tap on "Miso Ramen"
    3.  Recipe Detail Screen -> Review Ingredients & Instructions
    4.  Tap "Start Cooking" -> Cooking Mode Screen
    5.  Follow steps -> Complete Cooking.
*   **Searching for a Recipe:**
    1.  Open App -> Home Screen
    2.  Tap Search Bar or Search Icon in Bottom Nav -> Search & Filter Screen
    3.  Enter "Chicken pasta" -> Apply Filters (e.g., <30 mins)
    4.  View Search Results -> Tap on a desired recipe -> Recipe Detail Screen.
*   **Saving a Favorite:**
    1.  Browse/Search -> Find a recipe -> Recipe Detail Screen
    2.  Tap Heart Icon (top right) -> Recipe saved to Favorites.
    3.  Access via Bottom Nav -> Favorites Screen -> View saved recipe.
