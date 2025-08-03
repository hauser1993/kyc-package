# Publishing Your Custom Version of Ballerine Web UI SDK

## Prerequisites

1. **NPM Account**: You need an npm account. Create one at [npmjs.com](https://www.npmjs.com)
2. **NPM Login**: Run `npm login` in your terminal
3. **Git Repository**: Have your code in a Git repository (GitHub, GitLab, etc.)

## Steps to Publish

### 1. Update Package Configuration

I've already updated your `package.json` with placeholder values. You need to replace these with your actual information:

```json
{
  "name": "@hauser1993/kyc-sdk",
  "version": "1.0.0",
  "author": "Your Name <your-email@example.com>",
  "repository": {
    "type": "git",
    "url": "https://github.com/your-username/your-repo-name"
  }
}
```

**Replace:**
- `@hauser1993/kyc-sdk` is already set as your package name
- `your-email@example.com` with your actual email
- `your-username/your-repo-name` with your actual GitHub repository

### 2. Choose Your Package Name

**Your package is already configured as:**
```json
"name": "@hauser1993/kyc-sdk"
```

### 3. Update Documentation

I've updated the README.md, but you should:
- The package name `@hauser1993/kyc-sdk` is already set in the documentation
- Update any Ballerine-specific branding or references
- Add your own description and features

### 4. Build the Package

```bash
npm run build
```

This will create the `dist` folder with your compiled SDK.

### 5. Test Your Package Locally

Before publishing, test your package:

```bash
npm pack
```

This creates a `.tgz` file. You can install it locally to test:

```bash
npm install ./your-package-name-1.0.0.tgz
```

### 6. Publish to NPM

**First time publishing:**
```bash
npm publish
```

**For scoped packages (if you're not part of the organization):**
```bash
npm publish --access public
```

**Subsequent updates:**
```bash
npm version patch  # or minor/major
npm publish
```

### 7. Verify Publication

Check your package on npmjs.com:
```
https://www.npmjs.com/package/your-package-name
```

## Important Considerations

### Legal and Licensing
- Ensure you have the right to publish a derivative of Ballerine's code
- Check the original Ballerine license (likely MIT or similar)
- Consider adding your own license file if needed

### Attribution
- Consider adding attribution to the original Ballerine project
- Update the README to mention this is a custom version

### Version Management
- Start with version `1.0.0` for your first release
- Use semantic versioning for updates
- Consider using `npm version` commands for consistent versioning

### Package Scope
- Scoped packages (`@username/package-name`) are recommended for personal projects
- They help avoid naming conflicts
- They're free for public packages

## Example Commands

```bash
# Login to npm
npm login

# Build your package
npm run build

# Test locally
npm pack

# Publish (first time)
npm publish --access public

# For updates
npm version patch
npm publish
```

## Troubleshooting

**"Package name already exists"**
- Choose a different package name
- Use a scoped package name

**"Access denied"**
- Make sure you're logged in: `npm whoami`
- For scoped packages, use `--access public`

**"Invalid package name"**
- Package names must be lowercase
- No spaces, only hyphens and underscores
- Must start with a letter

## After Publishing

1. **Update your repository** with the published version
2. **Create a release** on GitHub/GitLab
3. **Update documentation** with installation instructions
4. **Test the published package** in a new project

## Example Usage After Publishing

```javascript
// Install your package
npm install @hauser1993/kyc-sdk

// Use it in your code
import { flows } from '@hauser1993/kyc-sdk';

await flows.init({
  // your configuration
});
``` 