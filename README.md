# react-components-starter

A React component library built with Tailwind CSS and tailwind-variants.

## Development

- Install dependencies:

```bash
npm install
```

- Run the playground:

```bash
npm run play
```

- Run the unit tests:

```bash
npm run test
```

- Build the library:

```bash
npm run build
```

- Run Storybook:

```bash
npm run storybook
```

## Usage in Your Project

### Installation

```bash
npm install @jim850221/react-components-starter
# or
yarn add @jim850221/react-components-starter
```


### Setup Tailwind CSS

This component library works with **both Tailwind v3 and v4**. Here's how to set it up:

1. Install Tailwind CSS (v3 or v4):

```bash
# For v3 (recommended for most projects)
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# OR for v4 (beta)
npm install -D tailwindcss@next @tailwindcss/postcss@next autoprefixer
```

2. **Import colors in your `tailwind.config.js`**:

```js
// tailwind.config.js
import { colors } from '@jim850221/react-components-starter/preset'

export default {
  content: [
    './src/**/*.{js,ts,jsx,tsx}',
    // Important: Include the component library's dist folder
    './node_modules/@johnny850221/react-components-starter/dist/**/*.js',
  ],
  theme: {
    extend: {
      colors: {
        ...colors,  // This adds primary-* and secondary-* colors
      },
    },
  },
  plugins: [],
}
```

3. In your main CSS file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

⚠️ **Important:** You must add the colors to your config (step 2) to use `primary-*` and `secondary-*` utility classes in your own code. The library's components will work automatically.

---

**Available custom colors:**
- `primary-*` (50-900) - Brand primary purple (#4E23A3)
- `secondary-*` (100-900) - Brand secondary gray

These colors extend (not replace) Tailwind's default colors.

4. (Optional) Extend with the library's theme preset in your `tailwind.config.js`:

```js
export default {
  presets: [
    require('@johnny850221/react-components-starter/tailwind.config')
  ],
  theme: {
    extend: {
      // Your custom theme
    },
  },
}
```

### Using Components

This package exports two main parts:

#### 1. UI Components

```tsx
// Import from the main entry (recommended)
import { MyButton } from '@jim850221/react-components-starter'

// Or import from the ui subpath
import { MyButton } from '@jim850221/react-components-starter/ui'

function App() {
  return (
    <div>
      <MyButton variant="primary" size="md">
        Click me
      </MyButton>
      <MyButton variant="secondary">
        Secondary
      </MyButton>
      <MyButton variant="outline" size="lg">
        Large Outline
      </MyButton>
    </div>
  )
}
```

#### 2. Design Tokens (ESM Export)

The package exports color tokens that you can use programmatically:

**Import color tokens in your JavaScript/TypeScript:**

```ts
import { colors } from '@jim850221/react-components-starter/preset'

// Use in your components programmatically
const MyComponent = () => (
  <div style={{ backgroundColor: colors.primary[500] }}>
    Styled with preset colors: {colors.primary[500]}
  </div>
)

// Or use in theme configuration
console.log(colors.primary[500]) // '#4E23A3'
```

**Available colors:**
- `colors.primary` - Purple color scale (50-900)
- `colors.secondary` - Gray color scale (100-900)

**This ESM export is:**
- ✅ Required for Tailwind v3 projects (must add to config)
- ✅ Optional for Tailwind v4 projects (colors already via `@theme`)
- ✅ Useful for programmatic color access in both versions
