# Publishing Guide

## Package Info

- **Name**: `autosizes`
- **Repository**: https://github.com/yournextagency/autosizes
- **Size**:
  - Source: 8.2 KB
  - Minified: 2.3 KB
  - Gzipped: 1.1 KB

## Publishing to npm

### Prerequisites

1. **npm account**: Create at https://www.npmjs.com/signup
2. **Login**: `npm login`
3. **Verify**: `npm whoami`

### Before Publishing

1. **Test build**:
   ```bash
   npm run build
   ```

2. **Verify files**:
   ```bash
   npm pack --dry-run
   ```

   Should include:
   - autosizes.js
   - autosizes.min.js
   - index.js
   - LICENSE
   - README.md
   - package.json

3. **Test locally**:
   ```bash
   npm pack
   # Creates autosizes-1.0.0.tgz
   # Test in another project:
   npm install /path/to/autosizes-1.0.0.tgz
   ```

### Publishing

```bash
# First time publish
npm publish

# Future updates
npm version patch  # 1.0.0 -> 1.0.1
npm version minor  # 1.0.0 -> 1.1.0
npm version major  # 1.0.0 -> 2.0.0
npm publish
```

## After Publishing

### CDN Links

Once published, the package will be automatically available on these CDNs:

#### unpkg (fastest, recommended)
```html
<!-- Latest version -->
<script type="module" src="https://unpkg.com/autosizes"></script>

<!-- Specific version -->
<script type="module" src="https://unpkg.com/autosizes@1.0.0/index.js"></script>

<!-- Minified -->
<script src="https://unpkg.com/autosizes@1.0.0/autosizes.min.js"></script>
```

#### jsDelivr (with fallback CDN)
```html
<!-- Latest version -->
<script type="module" src="https://cdn.jsdelivr.net/npm/autosizes"></script>

<!-- Specific version -->
<script type="module" src="https://cdn.jsdelivr.net/npm/autosizes@1.0.0/index.js"></script>

<!-- Minified -->
<script src="https://cdn.jsdelivr.net/npm/autosizes@1.0.0/autosizes.min.js"></script>
```

### Verify CDN Availability

After publishing, wait 5-10 minutes, then check:

- unpkg: https://unpkg.com/autosizes
- jsDelivr: https://cdn.jsdelivr.net/npm/autosizes

## GitHub Release

Create a GitHub release to match the npm version:

1. Go to: https://github.com/yournextagency/autosizes/releases/new
2. Tag: `v1.0.0`
3. Title: `v1.0.0 - Initial Release`
4. Description:
   ```markdown
   ## Features
   - Automatic `sizes` attribute calculation
   - Smart picture element support
   - Modern ES6 implementation
   - Only 2.3KB minified, 1.1KB gzipped

   ## Installation
   ```bash
   npm install autosizes
   ```

   ## CDN
   ```html
   <script type="module" src="https://unpkg.com/autosizes@1.0.0"></script>
   ```
   ```
5. Attach files:
   - autosizes.min.js
   - autosizes.js

## CDNJS (Optional)

For CDNJS inclusion, create a request at:
https://github.com/cdnjs/packages/issues

Requirements:
- Published to npm
- At least 800 stars on GitHub OR
- 200 downloads/week on npm

## Marketing

After publishing, announce on:
- Twitter/X
- Dev.to
- Reddit (r/webdev, r/javascript)
- Hacker News

Example tweet:
```
🚀 Just published autosizes - automatic sizes calculation for responsive images!

📦 Only 1.1KB gzipped
⚡️ Based on lazysizes
🎯 Modern ES6
✨ Zero config

npm install autosizes

https://github.com/yournextagency/autosizes
```

## Maintenance

### Update README on npm

After publishing, the README on npm will automatically update from the GitHub repo.

### Monitor

- npm downloads: https://npm-stat.com/charts.html?package=autosizes
- Bundle size: https://bundlephobia.com/package/autosizes
- GitHub stats: Watch stars, issues, PRs

### Support

- Issues: https://github.com/yournextagency/autosizes/issues
- Email: support@yournextagency.com (if applicable)

## Unpublishing (Emergency Only)

```bash
# Only within 72 hours of publishing
npm unpublish autosizes@1.0.0

# Deprecate instead (preferred)
npm deprecate autosizes@1.0.0 "Security issue, please upgrade"
```

**Note**: Never unpublish unless absolutely necessary (security issue). Use `npm deprecate` instead.
