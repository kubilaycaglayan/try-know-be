For "Wander" projectname the imported times seems to be repeating in the path history.

Imported Clockify session · 8/25/2026, 11:50:41 PM

Imported Clockify session · 8/25/2026, 11:50:41 PM

Imported Clockify session · 8/25/2026, 11:50:41 PM

Imported Clockify session · 8/25/2026, 11:50:41 PM

Imported Clockify session · 8/25/2026, 11:50:41 PM

Imported Clockify session · 8/25/2026, 11:50:41 PM

Imported Clockify session · 8/25/2026, 11:50:41 PM

You can check the data/clockify-july.json file to reason about times of the objects and map them correctly. Each session should have a start and end time and date.

Test with the given data.

Implemented in commit `032e1ff` (`fix: preserve imported clockify session intervals`).
