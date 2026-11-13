# Record schemas (JSONL, one record per line, `v` = schema version)
SI units always. Display conversion happens in the UI only.
Every record: {"id","v":1,"kind","ts":ISO-UTC save time,"tz":IANA,"date":"YYYY-MM-DD" logical day}
`date` is the day the entry is *for* (the app can back-date); `ts` is when it was saved.
Older body lines have no `date`; readers derive it from `ts` in `tz`.

body.jsonl      {...,"weight_kg"?,"waist_cm"?,"note"?}
nutrition.jsonl {...,"kcal","protein_g"?,"carbs_g"?,"fat_g"?}
  - Latest `ts` per `date` wins (re-saving a day = correction; old lines stay as history).
cardio.jsonl    {...,"activity","duration_s","distance_m"?,"avg_hr"?,"hard"?:true}
gym.jsonl       {...,"skipped":bool}   planned gym day marked "skipped as rest"; latest ts per date wins.
                A gym day counts as done when any lift/cardio record exists for that date (no record needed).
lift.jsonl      {...,"exercise_id","sets":[{"reps","weight_kg"} | {"duration_s"}]}
  - weight_kg is per dumbbell for per_side exercises; volume doubles it. Bodyweight exercises store added weight (0 = bodyweight only).
stretch.jsonl   {...,"morning_done":bool,"night_done":bool}
  - Latest `ts` per `date` wins; every toggle appends the full state for that day.
exercise.jsonl  {...,"exercise_id","name","pattern","per_side","bodyweight","timed"}   custom exercises added in the app

## Weekly plan: data/template.json (UI only, not a log)
{"updated":epoch-ms,"days":{"mon".."sun":{"name","note"?,"type":"lift|cardio|optional|rest",
  "cardio"?:{"label","desc"?,"suggested","allowed":[],"avoid":[],"minutes":[min,max],"intensity":"easy|any|hard_ok"},
  "items":[{"ex_ids":[primary,alt?],"sets","rep_min","rep_max","main"?,"superset"?,"note"?}]}}}
Whole file is replaced on edit; the copy with the newer `updated` wins on sync. Logs reference exercise_id,
so editing or replacing the plan never changes history.

## Deletes (tombstones)
Files are append-only. Deleting an entry appends {"id","v":1,"kind":<same kind>,"ts","tz","del":<id of deleted record>}
to that kind's file. Readers drop any record whose id appears in a `del`.
