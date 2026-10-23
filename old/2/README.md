# QuickScan v2 — Template designer + camera scanner

## Files
- `index.html`: 8.5 × 13 inch OMR sheet designer, configurable 10–200 questions, 10-item increments, two logo uploads, export JSON.
- `scanner.html`: live camera and photograph testing, OpenCV.js marker detection, perspective correction and bubble fill estimation, scan JSON export.

## Run
1. From this folder run `python -m http.server 8000` and open `http://localhost:8000/index.html`. For mobile devices use an **HTTPS** host; plain HTTP on a LAN will not provide camera access in modern browsers.
2. Set item count, school heading and both logos in designer; print on actual 8.5 × 13 inch paper at 100%. Export the scanner JSON alongside the printed page.
3. Open `scanner.html`, import the JSON, choose the printed page number and start the camera (or upload a photograph). An internet connection is required to download OpenCV.js from docs.opencv.org.
4. Position the whole sheet in the frame, with all four black tracking squares visible. Hold still for successive frames. Review uncertain responses before using them for grading.

## Important prototype limitations
- This is a **prototype**, not a validated grading system. It does not read student names, answer keys or QR codes, save records to a database, or assign examination scores.
- Four black corner squares are detected heuristically. Logos or other square shapes and background clutter may confuse detection. Validate against real photographs and add robust fiducial/marker verification before use in assessments.
- Thresholds and stability rules require calibration on actual paper, cameras, fonts, pencil shading and lighting.
- Scanner JSON uses the physical bubble centers from the designer; do not scale the printed sheet.
- Uploaded logos are deliberately limited to PNG/JPEG in v2 to avoid embedded active SVG contents.
- This version does not modify any separate locally edited copy of your original `index.html`. To preserve your own edits, compare/merge changes rather than overwriting blindly.
