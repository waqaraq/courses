# Course OS CDN visuals — Phase 1

This package matches `Config_CDN_Phase1.gs`.

## Upload layout
Upload the `2026.09` directory beneath your CDN root. Example:

```text
https://assets.example.edu/course-os/2026.09/lectures/w01/visual.svg
...
https://assets.example.edu/course-os/2026.09/lectures/w16/visual.svg
```

Then set in `Config_CDN_Phase1.gs`:

```javascript
"assets": {
  "baseUrl": "https://assets.example.edu/course-os",
  "version": "2026.09",
  "preferCdnVisuals": true,
  "visuals": {
    "enabled": true,
    "defaultKind": "svg",
    "pathTemplate": "lectures/{weekIdLower}/visual.svg"
  }
}
```

## Safe migration workflow
1. Upload all SVG files.
2. Set `assets.baseUrl`.
3. Verify the 16 URLs from `manifest.json` through your CDN/browser (HTTP 200).
4. Run `syncVisualizationsFromConfig()` if you changed any lecture visualization definitions in Config.gs.
5. Redeploy/test the Web App.

If an SVG is unavailable in a student's browser, the original `steps`/`compare` visual automatically appears instead.

## Per-lecture override
```javascript
"visualization": {
  "type": "steps",
  "title": "Example",
  "items": ["A", "B", "C"],
  "asset": {
    "kind": "image",
    "path": "lectures/w03/custom.webp",
    "alt": "Accessible description",
    "caption": "Optional caption"
  }
}
```

Set `"asset": false` on one visualization to force the generated fallback for that lecture.
