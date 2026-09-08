# Show newly uploaded product photos first

## What will change
- Sort the individual product-photo cards inside each shop category by their real upload time, newest first. This is the path currently missed: newly uploaded photos are saved as new child items with a larger display position, while the category page currently keeps that older position order.
- Keep the existing newest-first sorting inside detail pop-ups and image galleries.
- Use the upload timestamp already embedded in uploaded image addresses, with each item's saved creation time as a fallback, so older built-in images remain stable and no photos disappear.
- Apply the same order consistently to the visible category grid and any filtering of that grid; do not change product information, pot specifications, or unrelated page styling.

## Verification
- Open the category containing the latest uploaded image and confirm that image is the first card rather than the last.
- Open its details pop-up and confirm its images also remain newest-first.
- Check a category containing older built-in images to confirm its photos still display correctly.
- Confirm the site passes its build check and has no new browser errors.

## Technical details
- Add a reusable timestamp accessor alongside the existing image sorter, or sort product rows with a comparator that reads `/uploads/{timestamp}-...` and falls back to `created_at`.
- Sort a copied child-item array before converting it into the category's displayed items, avoiding mutation of cached backend data.
