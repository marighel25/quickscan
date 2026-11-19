# QuickScan v11 — Full Long-Bond OMR, No Database

## Files
- `index.html` — Full-page 8.5 × 13 inch (215.9 × 330.2 mm) portrait answer-sheet designer.
- `scanner.html` — OpenCV.js camera/photo scanner, automatic paper orientation correction, answer-key acquisition, student-ID OMR recognition, CSV roster matching, grading, and CSV score export.
- `students_template.csv` — Sample student roster format.

## Answer-sheet design
- Uses the **entire 8.5 × 13 inch long-bond paper**. The former 6.5 × 8.5 inch half-sheet format has been removed.
- Portrait orientation; one full-page answer sheet per long-bond sheet.
- Fixed 10-digit student-number OMR: ten digit columns, with choices 0–9 in each column.
- Dynamic answer columns: 1–20 questions uses one column, 21–40 uses two columns, and 41–60 uses three columns. Additional pages are generated for exams above 60 questions.
- Two customizable school/department logos.
- Four registration markers; the top-left marker has a white center to identify the physical top-left corner and support automatic orientation correction.
- The exported JSON contains the full-page physical marker and bubble coordinates. Always export a fresh JSON template after changing the design.

## Run
1. Extract the folder and run `python -m http.server 8000` from it.
2. Open `http://localhost:8000/index.html`. For phone-camera scanning from another device, host over HTTPS; camera access generally requires HTTPS or localhost.
3. Configure the exam and print using **8.5 × 13 inch long-bond paper, portrait, 100% / Actual size**. Disable “Fit to page”, printer headers, and footers.
4. Export the scanner JSON template and keep it with the printed exam.

## Examination workflow
1. Open `scanner.html`, import the matching JSON template, and select **Correct answer key** mode.
2. Shade the correct answers on a clean answer-key sheet. Scan each page, inspect the aligned image and recognized answers, and confirm each key page. Uncertain or multiple marks must be corrected and rescanned.
3. After all key pages are confirmed, import the student roster CSV.
4. Students shade exactly one digit (0–9) in each of the ten student-ID columns on every page. The scanner reads the 10-digit ID and matches it to the CSV roster.
5. Scan each student page. Check the recognized ID, inspect the detected answers, and accept the page. Multi-page exams are combined into a total score.
6. Export the scores CSV before closing or refreshing the browser.

## Student CSV
Required header: `Student ID`. Optional header: `Student Name`. Example:

```csv
Student ID,Student Name
0123456789,Juan Dela Cruz
1234567890,Maria Santos
```

Format Student ID as **Text** in Excel to preserve leading zeros. IDs must contain exactly ten digits. An ID not found in the roster, a blank digit column, or multiple shaded digits in a digit column is flagged for review.

## No database
No database or server-side record storage is used. The roster, answer key, and scores remain in browser memory for the active session. Export scores before leaving or reloading the page. OpenCV.js is loaded from its CDN, so the initial scanner load requires internet access unless OpenCV.js is hosted locally.

## Validation
JavaScript syntax and ZIP integrity can be checked programmatically, but real print alignment and camera recognition must be tested with actual long-bond printouts, different phones, pencil/pen marks, lighting, and all four paper orientations before using QuickScan for live examination grading. This prototype is not a substitute for supervised validation.


## v12 scanning-mode correction
- Answer Key mode reads answer bubbles only; student-number shading is not required or validated.
- Student Sheet mode reads the 10-digit ID and checks it against the imported roster before saving results.
- Scan results record their mode; answer-key scans show a clear message that student numbers are not required.


## v13 student-number alignment correction
- Corrected the 10-digit student-number bubble coordinates to match the actual compact right-column grid on the printed 8.5 × 13 inch sheet.
- Student ID bubble centers now start at X=136.85 mm and Y=78.00 mm, with 5.70 mm column pitch and 3.50 mm row pitch.
- Export a new JSON template from the updated designer and use that same template when scanning newly printed v13 sheets. Do not mix older printed sheets or JSON templates with this version.


## v23 student-number alignment correction
- Corrected the student ID bubble Y-coordinate in exported template metadata from 78.0 mm to 74.85 mm to match the actual printed grid position.
- The change moves scanner diagnostic circles upward by 3.15 mm so they align with the centers of the printed student-number bubbles.
- Answer-choice layout and student-number bubble design are unchanged.
