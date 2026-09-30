# Training (web) – Push / Pull / Legs / Core & Cardio log

English web version of the Android app [training](https://github.com/ZweiSebastian/training), for iPhone.
Open the page in Safari → Share → **Add to Home Screen**.

- **Workout**: today's plan from the weekly schedule; per exercise "Last time" + "Strongest" + input (kg / reps / + Set).
- **History**: all workouts, filterable, tap = edit.
- **Plan**: weekly schedule, exercises per day, cloud backup with recovery code.

Notation: `20×12 // 80×12 // 120×12 / 10 / 8+1`

Data lives on the phone (localStorage) and is backed up to its own Supabase tables (`training_gia_backups`, `training_gia_snapshots`), separate from the Android app.
