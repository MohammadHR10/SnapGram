# React + TypeScript + Tailwind CSS Setup Guide

## 1. Project Initialization

```bash
# Create a new Vite project with React and TypeScript
npm create vite@latest my-project -- --template react-ts

# Navigate to project directory
cd my-project

# Install dependencies
npm install
```

## 2. Tailwind CSS Setup

### Install Required Packages

```bash
# Install specific versions for better compatibility
npm install -D tailwindcss@3.3.0 postcss@8.4.31 autoprefixer@10.4.14
```

### Create Configuration Files

1. Create `postcss.config.cjs`:

```javascript
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

2. Create `tailwind.config.cjs`:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: ["class"],
  content: [
    "./pages/**/*.{ts,tsx}",
    "./components/**/*.{ts,tsx}",
    "./app/**/*.{ts,tsx}",
    "./src/**/*.{ts,tsx}",
  ],
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        "primary-500": "#877EFF",
        "primary-600": "#5D5FEF",
        "secondary-500": "#FFB620",
        "off-white": "#D0DFFF",
        red: "#FF5A5A",
        "dark-1": "#000000",
        "dark-2": "#09090A",
        "dark-3": "#101012",
        "dark-4": "#1F1F22",
        "light-1": "#FFFFFF",
        "light-2": "#EFEFEF",
        "light-3": "#7878A3",
        "light-4": "#5C5C7B",
      },
      screens: {
        xs: "480px",
      },
      width: {
        420: "420px",
        465: "465px",
      },
      fontFamily: {
        inter: ["Inter", "sans-serif"],
      },
      keyframes: {
        "accordion-down": {
          from: { height: 0 },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: 0 },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [],
};
```

### Set up CSS

1. Create or update `src/globals.css`:

```css
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap");

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  * {
    @apply box-border list-none p-0 m-0 scroll-smooth;
  }

  body {
    @apply bg-dark-1 text-white min-h-screen font-inter;
  }
}

/* Add your custom styles here */
```

2. Import the CSS in your main component (`src/App.tsx`):

```typescript
import "./globals.css";

const App = () => {
  return (
    <div className="min-h-screen bg-gray-900 text-white">
      {/* Your components here */}
    </div>
  );
};

export default App;
```

## 3. Project Structure

```
my-project/
├── src/
│   ├── components/     # React components
│   ├── pages/         # Page components
│   ├── App.tsx        # Main App component
│   ├── main.tsx       # Entry point
│   └── globals.css    # Global styles
├── public/            # Static assets
├── index.html         # HTML template
├── package.json       # Dependencies and scripts
├── postcss.config.cjs # PostCSS configuration
├── tailwind.config.cjs # Tailwind configuration
├── tsconfig.json      # TypeScript configuration
└── vite.config.ts     # Vite configuration
```

## 4. Common Issues and Solutions

### Issue: Module System Conflicts

If you see errors about ES modules vs CommonJS:

- Use `.cjs` extension for config files
- Use `module.exports` instead of `export default` in config files

### Issue: Tailwind Not Working

1. Check if `globals.css` is imported in your main component
2. Verify that Tailwind directives are present in `globals.css`
3. Ensure config files are in the correct location
4. Check for version compatibility issues

### Issue: TypeScript Errors

1. Make sure `tsconfig.json` includes all necessary paths
2. Add type declarations for CSS modules if needed:

```typescript
// src/vite-env.d.ts
/// <reference types="vite/client" />
```

## 5. Development

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## 6. Additional Tips

1. **Custom Classes**: Define reusable classes in `globals.css` using `@layer components`
2. **Theme Customization**: Add custom colors, fonts, and other theme values in `tailwind.config.cjs`
3. **Responsive Design**: Use Tailwind's responsive prefixes (sm:, md:, lg:, xl:)
4. **Dark Mode**: Configure dark mode in `tailwind.config.cjs` and use `dark:` prefix

## 7. Useful Resources

- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Vite Documentation](https://vitejs.dev/guide/)
- [React Documentation](https://react.dev/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
