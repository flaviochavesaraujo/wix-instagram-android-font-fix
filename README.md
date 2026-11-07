# Wix Studio: Fixing Text Overlap in Instagram's Android In-App Browser

**A Technical Investigation by FCA Coders — Brazil**

**Status:** Successfully tested on two Samsung Android devices  
**Date:** November 6, 2026  
**Platform:** Wix Studio / Instagram Android In-App Browser

## 1. The Problem

During mobile testing of a Wix Studio website, we discovered a rendering issue affecting text and image positioning when the website was opened through Instagram's built-in browser on Android devices.

The same pages displayed correctly in:

- Google Chrome on Android
- Instagram's in-app browser on iPhone
- Wix Studio's mobile preview

However, Instagram's in-app browser on Android enlarged text unexpectedly, causing overlapping elements and broken layouts.

The issue was reproduced on two Samsung smartphones.

## 2. Identifying the Trigger

Our investigation revealed a direct relationship between Android system font settings and the rendering problem.

| Test | Result |
|---|---|
| Original Android font size | Text overlap occurred |
| Reduced Android font size | Layout displayed correctly |
| Restored original font size | Overlap returned |
| Chrome on Android | Displayed correctly |
| Instagram on iPhone | Displayed correctly |

These results strongly suggested that Android WebView text scaling was involved.

## 3. Unsuccessful Attempts

Before finding a working solution, we performed several controlled experiments:

- Removed containers and stacked elements.
- Rebuilt the affected page using only three text elements and one image.
- Tested different grid dimensions and responsive units.
- Applied CSS `text-size-adjust: 100%`.
- Tested opening Chrome through an Android Intent.

Removing containers and simplifying the layout did not eliminate the problem.

The Android Intent approach opened Chrome successfully but required an additional confirmation from Instagram, making it less suitable for our users.

## 4. The Solution That Worked

We tested the following HTML meta tag:

```html
<meta name="text-scale" content="scale">
```

This feature is associated with modern Chromium-based Android WebView text scaling behavior.

### How to Apply It in Wix Studio

1. Open your Wix Studio editor.
2. Navigate to **Pages**.
3. Open the settings of the affected page.
4. Select **Advanced SEO**.
5. Expand **Additional Tags**.
6. Click **Add New Tag**.
7. Add the meta tag with:
   - Name: `text-scale`
   - Content: `scale`
8. Save and publish your changes.

Test the page through Instagram's in-app browser on Android.

**Important:** Meta tags configured for a specific Wix page do not automatically apply to every other page.

## 5. Validation Results

After applying the meta tag, the text overlap disappeared in our testing environments.

We validated the solution using:

- Two Samsung Android smartphones.
- Two different Instagram accounts.
- Android with enlarged system font settings.
- An iPhone, which continued displaying the website correctly.

Following these successful tests, we applied the meta tag across the pages of our Wix Studio website.

**The fix worked in our tested environments, but universal compatibility has not been established.**

## 6. Accessibility and Compatibility

The `text-scale` meta tag is a relatively recent browser feature with limited compatibility across browsers and versions.

Developers should:

- Test on multiple Android devices.
- Verify rendering with enlarged system font settings.
- Confirm that users can still read and enlarge content appropriately.
- Test other browsers and operating systems.
- Avoid treating this as a guaranteed universal solution.

The goal is to prevent unexpected layout breakage while preserving accessibility.

## 7. Technical References

- [MDN — HTML text-scale meta tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta/name/text-scale)
- [Wix Help Center — Adding Custom Meta Tags](https://support.wix.com/en/article/adding-custom-meta-tags-to-your-site)
- [Wix Studio Community](https://forum.wixstudio.com/)

## 8. Final Conclusions

Our experiments demonstrated that removing containers, rebuilding page structures, and changing responsive dimensions were not sufficient to fix the issue.

The successful workaround was the HTML meta tag:

```html
<meta name="text-scale" content="scale">
```

We hope this investigation helps other developers experiencing similar problems with Wix Studio websites inside Instagram's Android in-app browser.

If you test this solution, please share your device model, browser version, and results.

Every additional test can help improve our understanding of this issue.

---

**FCA Coders — Brazil**

*Engineering • Research • Development • Testing*

**Our principle:** A technical solution becomes more valuable when it can be documented, reproduced, and shared.
