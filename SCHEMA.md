# Record schemas (JSONL, one record per line, `v` = schema version)
SI units always. Display conversion happens in the UI only.

body.jsonl      {"id","v":1,"kind":"body","ts":ISO-UTC,"tz":IANA,"weight_kg"?,"waist_cm"?,"note"?}
nutrition.jsonl {"id","v":1,"kind":"nutrition","ts","tz","date":"YYYY-MM-DD","kcal","protein_g","carbs_g","fat_g"}
  - Latest `ts` per `date` wins (re-saving a day = correction; old lines stay as history).
Next: workouts.jsonl (per-set, exercise_id references exercises.json), cardio in the same file.
