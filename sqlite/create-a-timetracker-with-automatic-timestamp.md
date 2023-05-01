# Create a Timetracker With Automatic Timestamp


1. Open a new file:

```bash
sqlite timetracker.db
```

2. Create a table:

```sql
CREATE TABLE language_tracker (
    id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
    activity TEXT,
    time_spend INTEGER,
    datetime DATETIME DEFAULT datetime(CURRENT_TIMESTAMP, 'localtime') NOT NULL
);

```

3. Add new information into the table:

```sql
INSERT INTO `language_tracker` (activity, datetime)
    VALUES ('Dreaming Spanish Beginner', 33) # I spend 33 minutes immersing in "Dreaming Spanish"
```

The entry will have a timestamp that looks like this: `2023-04-30 17:59:08`.
