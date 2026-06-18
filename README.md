# Linear Algebra Drills

A free, no-backend quiz app for linear algebra practice. Students open a link
(or scan a QR code) on their phone, pick a concept, and drill through
multiple choice / type-the-answer / word-bank questions. Scores are stored
locally in each student's browser — no accounts, no server, no cost.

## 1. Put this on GitHub Pages (one-time setup, ~5 minutes)

1. Create a new repository on GitHub (e.g. `linalg-drills`). Public repos
   get free Pages hosting.
2. Upload these files keeping the folder structure:
   ```
   index.html
   decks/manifest.json
   decks/vectors-basics.json
   decks/matrix-operations.json
   ```
   Easiest way: on the repo page, click "Add file" → "Upload files", drag
   the whole `linalg-quiz` folder contents in, commit.
3. Go to the repo's **Settings → Pages**. Under "Build and deployment",
   set Source to "Deploy from a branch", branch `main`, folder `/ (root)`.
   Save.
4. After a minute, GitHub shows your live URL, something like:
   ```
   https://YOUR-USERNAME.github.io/linalg-drills/
   ```
   That's the link students use. Bookmark it.

You're done with setup. Everything from here on is just editing JSON files.

## 2. Adding a new deck (a new concept)

A deck is one JSON file in the `decks/` folder, plus one line in
`decks/manifest.json` so the app knows it exists.

**Step A** — Create a new file, e.g. `decks/eigenvalues.json`:

```json
{
  "id": "eigenvalues",
  "title": "Eigenvalues & Eigenvectors",
  "description": "Finding eigenvalues, characteristic polynomial",
  "questions": [
    {
      "type": "mc",
      "prompt": "An eigenvector of A satisfies which equation?",
      "choices": ["Av = v", "Av = \u03bbv", "A + v = \u03bb", "Av = 0"],
      "answer": 1
    },
    {
      "type": "type",
      "prompt": "What are the eigenvalues of a diagonal matrix? (one word)",
      "answer": ["diagonal", "the diagonal entries"]
    },
    {
      "type": "wordbank",
      "prompt": "The _____ polynomial is found by det(A - \u03bbI) = 0.",
      "wordbank": ["characteristic", "minimal", "cubic", "augmented"],
      "answer": "characteristic"
    }
  ]
}
```

**Step B** — Add it to `decks/manifest.json`:

```json
[
  { "id": "vectors-basics", "file": "decks/vectors-basics.json" },
  { "id": "matrix-operations", "file": "decks/matrix-operations.json" },
  { "id": "eigenvalues", "file": "decks/eigenvalues.json" }
]
```

**Step C** — Commit both files on GitHub. Refresh the page — the new deck
card appears automatically. No code changes, ever, needed.

### Question type reference

**Multiple choice** (`"type": "mc"`)
- `choices`: array of option strings
- `answer`: the **index** (0, 1, 2...) of the correct option

**Type-the-answer** (`"type": "type"`)
- `answer`: an array of acceptable strings (covers alternate phrasings/typos
  you want to allow). Matching ignores case and surrounding spaces.

**Word bank** (`"type": "wordbank"`)
- `prompt`: must contain `_____` (five underscores) where the blank goes
- `wordbank`: array of word choices shown as tappable chips (include
  distractors)
- `answer`: the one correct word, exactly as it appears in `wordbank`

## 3. Making the QR code

Once your GitHub Pages URL is live, generate a QR code for free at
[qr-code-generator.com](https://www.qr-code-generator.com/) or
[qrcode-monkey.com](https://www.qrcode-monkey.com/) — paste in your URL,
download the PNG, put it on a slide or handout.

**Tip:** you can link directly to one deck by adding `?deck=<id>` to the
URL, e.g.:
```
https://YOUR-USERNAME.github.io/linalg-drills/?deck=eigenvalues
```
Handy if you want a different QR code per week/topic, all pointing at the
same app.

## 4. What's already built vs. what's next

**Working now:** deck menu, all three question types, per-deck best score
saved on-device, progress bar, results screen.

**Natural next steps** (ask me anytime — each is a separate small build):
- Local leaderboard (compare scores with classmates using a free backend
  like Firebase or Supabase free tier)
- Timed mode / streaks
- Export deck authoring to a Google Sheet instead of hand-editing JSON
- Dark/light theme toggle
