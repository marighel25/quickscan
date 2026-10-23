# QuickScan v3 — Half-sheet OMR

- `index.html`: 6.5 × 8.5 inch portrait OMR answer sheet; two rotated sheets per 8.5 × 13 inch printing page; up to 40 questions per half-sheet, increments of 10, up to 200 across multiple sheets. Two customizable logos.
- `scanner.html`: existing OpenCV.js camera/photo scanner retained, dynamically reads exported marker and bubble coordinates. Marker geometry estimator updated for half-sheet.

## How to use
1. Open index.html using an HTTP server, customize the two logos, heading, question count and exam code.
2. Export the matching JSON template.
3. Print at **100% Actual size** on **8.5 × 13 inch long bond** paper, without browser headers/footers or fit-to-page. Print CSS rotates and lays out two half-sheets on each long-bond page. Cut precisely along the center at 6.5 inches of the 13-inch side.
4. In scanner.html, load the newly exported JSON (old full-page templates do not match the new print), then test using uploaded photos or HTTPS smartphone camera.
5. Make sure all four square markers are visible. Inspect the corrected image and all uncertain marks before relying on any response.

## Limitations
This is a prototype, not a validated grading solution. The scanner still uses the same four-square corner detection and per-option ink-fill baseline. Real-world lighting, marked bubbles, camera models, and print scaling require calibration and evaluation. Camera access requires HTTPS/localhost. OpenCV.js loads from the internet unless hosted locally. Answer key grading and student record integration are not included.
