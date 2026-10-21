# Training (web) – Push / Pull / Legs / Core & Cardio log

English web version of the Android app [training](https://github.com/ZweiSebastian/training), for iPhone.
Open the page in Safari → Share → **Add to Home Screen**.

- **Workout**: today's plan from the weekly schedule; per exercise "Last time" + "Strongest" + input (kg / reps / + Set).
- **Weights in lb**: tap "kg" next to the weight field → "lb". Remembered per exercise (`lb` in the data, exercise names in lower case); the input is converted to kg (0.1 kg) and shown as "= x kg". Always saved and compared in kg; in lb mode the grey suggestion is shown in lb (rounded to 0.5 lb).
- **Run (treadmill)**: its own entry per day – sections with level + minutes (usually 3, "+ Section" for more), effort 1–10 and pain/discomfort. Grey = values from the last run, "Same as last time". On the Workout tab (also below an open workout).
- **History**: all workouts and runs, filterable, tap = edit.
- **Plan**: weekly schedule, exercises per day, cloud backup with recovery code.

Notation: `20×12 // 80×12 // 120×12 / 10 / 8+1`

Data lives on the phone (localStorage) and is backed up to its own Supabase tables (`training_gia_backups`, `training_gia_snapshots`), separate from the Android app.

## Merging with Supabase (no more overwriting)

Like the Android app: on every opening and before every upload the page first fetches the cloud state and merges it with the phone (three-way merge against the last common state `training-gia-base` in localStorage): changed only in the cloud → taken over · changed only on the phone → uploaded · same spot changed differently on both → cloud wins. Lists with `id` (or `date`) are merged entry by entry.

**For edits directly in the database** (e.g. by Claude): change `data` in `training_gia_backups` with `jsonb_set` and keep the existing `id`s. Runs live in `runs[]`: `{"id", "date", "created", "note", "rpe", "schmerz", "abschnitte": [{"stufe": 6.5, "min": 10}, …]}`.
