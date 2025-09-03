# Dependency Installation Issues and Solutions

This document outlines the dependency installation issues encountered with this project and their solutions.

## Issues Resolved

### 1. Node-sass Compatibility Issue

**Problem**: The original `node-sass@4.14.1` was incompatible with Node.js v22.14.0, causing Python syntax errors during installation.

**Solution**: Replaced `node-sass` with `sass` (Dart Sass) which is the recommended replacement.

**Changes Made**:
- Updated `package.json` to use `sass@^1.69.0` instead of `node-sass@^4.7.2`
- Updated build scripts to use `sass` command instead of `node-sass`
- Changed CSS build commands:
  - `css`: `sass src/scss/style.scss src/res/style.css`
  - `css:watch`: `npm run css && sass --watch src/scss/style.scss:src/res/style.css`

### 2. RobotJS Compatibility Issue

**Problem**: The `robotjs` package (from the custom fork) is incompatible with Node.js v22.14.0 due to V8 API changes.

**Current Status**: The dependency is included in package.json but may fail to install on Node.js v22+.

**Solutions**:

#### Option 1: Use Compatible Node.js Version (Recommended)
Use Node.js v16 or v18 which are compatible with the current robotjs version:

```bash
# Using nvm (Node Version Manager)
nvm install 16
nvm use 16
yarn install
```

#### Option 2: Install Without RobotJS (Development Only)
For development work that doesn't require robot functionality:

```bash
# Remove robotjs temporarily
yarn remove robotjs
yarn install
# Add it back when needed
yarn add git+https://github.com/jeremija/robotjs.git#71bb8aa
```

#### Option 3: Use Alternative Robot Control Library
Consider migrating to a more modern alternative like:
- `@nut-tree/nut-js` - Cross-platform native GUI automation
- `puppeteer` - For web automation
- Custom native modules with newer Node.js compatibility

## Installation Instructions

### For Development (Node.js v22)
```bash
# Install dependencies without robotjs
yarn install --ignore-optional
# Or temporarily remove robotjs from package.json
```

### For Production (Recommended)
```bash
# Use Node.js v16 or v18
nvm use 16  # or nvm use 18
yarn install
```

## Build Process

The build process now works correctly with the updated dependencies:

```bash
# Build CSS and JS
yarn build

# Watch for changes
yarn start:watch

# Run development server
yarn start:server
```

## Warnings

You may see deprecation warnings during the CSS build process. These are normal and don't affect functionality:
- Sass @import rules deprecation
- Global built-in functions deprecation
- Color functions deprecation

These warnings can be addressed in future updates by migrating to the newer Sass syntax.