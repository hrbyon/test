[README.md](https://github.com/user-attachments/files/31631610/README.md)
# CH40051 Electroanalytical Chemistry — companion site

Interactive materials for CH40051, Fall 2026. Static HTML: no build step, no
dependencies, no server-side code. Published with GitHub Pages from this repo's
root on the `main` branch.

## Pages

| File | Purpose |
|---|---|
| `index.html` | Course hub — the only link students need |
| `lecture01.html` | Lecture 1: Cell Builder, Faraday Bench, Concept Check |

## How releases are staged

Lecture pages are built well ahead of time but only go live on the morning of
the lecture. So this folder holds two kinds of hub file:

| File | What it is |
|---|---|
| `index.html` | **Mirrors what is live right now.** Do not upload; it is the reference copy. |
| `index NN.html` | The hub as it should look **once lecture NN is released**. |

### Releasing lecture NN

1. Upload `lectureNN.html`.
2. Upload `index NN.html`, **renaming it to `index.html`** — strip the space and
   the number. GitHub serves `index.html` as the directory index; a file called
   `index 02.html` is just another page nobody visits.
3. Update the local `index.html` to match what you just published, so the
   mirror stays honest.

Pages redeploys in about a minute. The hub URL never changes, so students keep
one bookmark all semester.

### Preparing the next one

Copy the current `index.html` to `index NN.html`, turn that lecture's
`<div class="lect soon">` block into `<a class="lect" href="lectureNN.html">`,
and change its `state soon` badge to `state live`.

## Concept Check result files

Each student downloads a one-row CSV and submits it to the LMS:

```
lecture,student_id,completed_utc,score,total,percent,verification,a1..a6,ok1..ok6
```

`verification` is an FNV-1a hash of `student_id|completed_utc|answer indices`.
It detects casual editing of a result file; it is **not** a security guarantee.
The reading tool recomputes each score from the answers, so editing the `score`
column alone changes nothing.

## Deliberately not in this repository

The **instructor console** that reads those CSVs is kept out of this repo. It
carries the answer key and the per-distractor teaching notes, and everything
here is world-readable once Pages is on. It runs entirely in the browser, so it
is opened from disk instead — no hosting required.

Students can already read the answer key out of any page's source; that is
inherent to a client-side quiz, and the reason these checks are formative only.
Grades come from the LMS.
