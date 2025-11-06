# Pre-commit Code Formatting with Husky and lint-staged

This guide will help you set up automatic code formatting using Husky and lint-staged to ensure consistent code style in your project before every commit.

## Prerequisites

- Node.js project with `package.json`
- Git initialized in your project

## Setup Instructions

### 1. Install Required Packages

Install the necessary development dependencies:

```bash
# Using npm
npm install --save-dev husky lint-staged prettier

# Or using Yarn
yarn add --dev husky lint-staged prettier
```

### 2. Initialize Husky

Set up Husky and create the required configuration files:

```bash
# Using npm
npx husky init && npm install

# Or using Yarn
yarn husky init && yarn install
```

This will:

- Create a `.husky` directory
- Add a sample `pre-commit` hook
- Add a `prepare` script to your `package.json`

### 3. Configure lint-staged

Add the following configuration to your `package.json`:

```json
{
  // ... other configurations
  "lint-staged": {
    "*.{js,jsx,ts,tsx,json,css,md}": ["prettier --write"]
  }
}
```

This configuration will run Prettier on all staged files with the specified extensions.

### 4. Configure Husky Pre-commit Hook

Update the `.husky/pre-commit` file with the following content:

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
# or use: yarn lint-staged
```

Make the file executable (if needed):

```bash
chmod +x .husky/pre-commit
```

### 5. Test Your Setup

1. Make a change to a file that violates your formatting rules
2. Stage the changes:
   ```bash
   git add .
   ```
3. Create a commit:
   ```bash
   git commit -m "Test husky commit"
   ```

The pre-commit hook will automatically format your staged files before the commit is created.

## Bypassing Hooks (When Needed)

To bypass the pre-commit hook (use sparingly):

```bash
git commit -m "Your commit message" --no-verify
```

## Troubleshooting

- If you encounter permission issues, ensure the pre-commit hook is executable
- Verify that all dependencies are installed correctly
- Check your editor's settings to ensure it's not conflicting with Prettier
