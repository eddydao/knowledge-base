`npx create-expo-app@latest ./`

`npm run ios`

`npm run reset-project`

# Styling 

## Nativewind
Using Tailwind CSS in React Native

Install package and lib that will help styling easier: 
`npm install nativewind tailwindcss react-native-reanimated react-native-safe-area-context`

`npx tailwindcss init` : generate configuration file `tailwind.config.ts`

Set content to the `tailwind.config.ts` file with content from **Nativewind** 

```typescript
/** @type {import('tailwindcss').Config} */
module.exports = {
  // NOTE: Update this to include the paths to all of your component files.
  content: ["./app/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Customize the `metro.config.js` file by create the file with `npx expo customize` and put these code below:

```javascript
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require('nativewind/metro');

const config = getDefaultConfig(__dirname)

module.exports = withNativeWind(config, { input: './global.css' })
```



# Routing
Work similarly like React
The files in the `app` folder represent the routes, and the file name is a route.

## Link from expo-router
`import {Link} from "expo-router`

`<Link href=""></Link>`

Create a dynamic route in React Native with `[ ]`in the file name:
eg: `[id]-movies.tsx`

`<Link href="/path/id`/>

Define `id` item to hold the id value
`const {id} = useLocalSearchParams()`

