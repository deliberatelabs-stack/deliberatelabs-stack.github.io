# Testing Guide

This document contains information for testing and verification of the CiteLens MCP documentation site.

## Site URLs

- **Home**: https://deliberatelabs-stack.github.io/
- **Docs**: https://deliberatelabs-stack.github.io/docs/
- **OAuth Callback**: https://deliberatelabs-stack.github.io/oauth/callback/
- **Sitemap**: https://deliberatelabs-stack.github.io/sitemap.xml
- **Robots.txt**: https://deliberatelabs-stack.github.io/robots.txt

## IndexNow Configuration

- **Key**: `909069aaec69db931d46b26b6cc5af14`
- **Key File URL**: https://deliberatelabs-stack.github.io/909069aaec69db931d46b26b6cc5af14.txt

### Testing IndexNow Submission

Once the site is live, you can test IndexNow submission:

```bash
# Test via GET (single URL)
curl "https://api.indexnow.org/indexnow?url=https://deliberatelabs-stack.github.io/&key=909069aaec69db931d46b26b6cc5af14"

# Test via POST (batch)
curl -X POST "https://api.indexnow.org/indexnow" \
  -H "Content-Type: application/json" \
  -d '{
    "host": "deliberatelabs-stack.github.io",
    "key": "909069aaec69db931d46b26b6cc5af14",
    "keyLocation": "https://deliberatelabs-stack.github.io/909069aaec69db931d46b26b6cc5af14.txt",
    "urlList": [
      "https://deliberatelabs-stack.github.io/",
      "https://deliberatelabs-stack.github.io/docs/"
    ]
  }'
```

Expected responses:
- `200` – URL submitted successfully
- `202` – URL received, key validation pending

## Bing Webmaster Tools Verification

To verify this site in Bing Webmaster Tools:

1. Go to https://www.bing.com/webmasters
2. Add site: `https://deliberatelabs-stack.github.io/`
3. Choose **XML File** verification method
4. Download the `BingSiteAuth.xml` file provided by Bing
5. Add it to the root of this repository
6. Push to main and wait for GitHub Pages to deploy
7. Click "Verify" in Bing Webmaster Tools

**Note**: Do not create a fake `BingSiteAuth.xml` file. It must contain the exact content provided by Bing during verification.

## OAuth Callback Testing

The OAuth callback page at `/oauth/callback/` is a static HTML page that displays `code` and `state` query parameters (or errors) on screen. It does not transmit data anywhere.

Test URL examples:
- Success: `https://deliberatelabs-stack.github.io/oauth/callback/?code=abc123&state=xyz`
- Error: `https://deliberatelabs-stack.github.io/oauth/callback/?error=access_denied&error_description=User%20denied`

Use this callback URL when registering OAuth applications for testing.

## GitHub Pages Setup

Ensure GitHub Pages is configured:

1. Go to **Settings → Pages** in the repository
2. Set **Source** to **Deploy from a branch**
3. Set **Branch** to `main` and folder to `/ (root)`
4. Save

The site should be available at https://deliberatelabs-stack.github.io/ within a few minutes.
