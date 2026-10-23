# QuickScan v3 — Half-sheet OMR

- `index.html`: 6.5 × 8.5 inch portrait OMR answer sheet; two rotated sheets per 8.5 × 13 inch printing page; up to 60 questions per half-sheet, increments of 10, up to 200 across multiple sheets. Two customizable logos.
- `scanner.html`: existing OpenCV.js camera/photo scanner retained, dynamically reads exported marker and bubble coordinates. Marker geometry estimator updated for half-sheet.

## How to use
1. Open index.html using an HTTP server, customize the two logos, heading, question count and exam code.
2. Export the matching JSON template.
3. Print at **100% Actual size** on **8.5 × 13 inch long bond** paper, without browser headers/footers or fit-to-page. Print CSS rotates and lays out two half-sheets on each long-bond page. Cut precisely along the center at 6.5 inches of the 13-inch side.
4. In scanner.html, load the newly exported JSON (old full-page templates do not match the new print), then test using uploaded photos or HTTPS smartphone camera.
5. Make sure all four square markers are visible. Inspect the corrected image and all uncertain marks before relying on any response.

## Limitations
This is a prototype, not a validated grading solution. The scanner still uses the same four-square corner detection and per-option ink-fill baseline. Real-world lighting, marked bubbles, camera models, and print scaling require calibration and evaluation. Camera access requires HTTPS/localhost. OpenCV.js loads from the internet unless hosted locally. Answer key grading and student record integration are not included.

## Dynamic answer columns (v4)
- Each half-sheet supports 20 questions per column and up to three columns (60 total).
- 10–20 questions: one centered column; 30–40: two centered columns; 50–60: three columns.
- If a page is partial, the last page uses only the number of columns it needs.
- The printed layout and exported JSON use the same computed bubble coordinates. Export a NEW JSON after any changes to the question count, and import it in scanner.html.
- Physical printer and camera testing is still required before using results for grading.
