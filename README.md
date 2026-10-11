# Lesson Reporting & Analytics System

A lightweight data system I designed and deployed for the Mathematics Department of a senior high school in Ghana. Teachers submit a short report after every lesson from their phones, and the Head of Department gets a live view of lessons taught, attendance and syllabus coverage, replacing paper logbooks.

**▶ Live demo:** https://augustine-akrasi.github.io/lesson-reporting-system/
*(Demo version: all teachers and students are fictional, and submissions are not saved.)*

---

## The problem

Heads of Department in Ghanaian senior high schools typically track teaching through paper records collected weeks after the fact. That makes it hard to answer simple questions in time to act:

- Which classes are falling behind the syllabus?
- Which students keep missing lessons?
- Where are students struggling on assessments?

## What the system does

**Teacher-facing form** (mobile-first, works on low-end phones)
- Records teacher, class, date, period, topic and syllabus coverage (completed / partial / not covered)
- Class register with one-tap Present/Absent, bulk marking, search, and a live attendance percentage
- Optional assessment capture: type, total marks, per-student scores with automatic percentage colour-coding, and the areas where students struggled
- Client-side validation, then a single structured JSON record per lesson

**Backend and dashboard**
- A Google Apps Script web app receives each record and appends it to Google Sheets, which acts as the database
- A Head of Department dashboard summarises syllabus coverage, attendance trends and assessment performance by class and teacher

## Architecture

```
Teacher's phone ──► HTML/JS form ──► Google Apps Script web app ──► Google Sheets
                                                                       │
                                     Head of Department dashboard ◄────┘
```

## Example record

Every submission produces one JSON record like this (submit the demo form to see a live one):

```json
{
  "formType": "post-lesson-report",
  "teacher": "Teacher A (demo)",
  "class": "2 Science",
  "date": "2026-10-11",
  "period": "Period 2 (8:00am – 9:00am)",
  "topic": "Indices",
  "coverage": "Completed",
  "attendance": { "presentCount": 11, "absentCount": 1, "totalMarked": 12, "rate": 92 },
  "assessment": { "type": "Quiz / pop quiz", "maxScore": 20, "averagePercent": 68,
                  "weakAreas": "Algebra manipulation, Word problems" },
  "submittedAt": "2026-10-11T08:55:12.000Z"
}
```

## Tech stack

HTML · CSS · vanilla JavaScript · Google Apps Script · Google Sheets · Netlify / GitHub Pages

## Privacy

This repository contains **no real school data**. All names in the demo roster are fictional, and the backend URL is left empty so the demo never sends data anywhere. In production, student rosters should be served from the protected backend rather than embedded in a public page.

## Roadmap

- Add the Apps Script backend and dashboard source to this repository
- Monthly automated analysis of attendance, syllabus coverage and assessment performance
- A second version for SHS 1, possibly built on KoboCollect for offline data capture

## Author

**Augustine Akrasi**: Mathematics educator & data scientist (MSc Data Science)
[LinkedIn](https://www.linkedin.com/in/augustine-akrasi-3ba695358) · [GitHub](https://github.com/augustine-akrasi)
