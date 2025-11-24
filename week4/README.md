# Week 4


# Joining Tables

``` python
import pandas as pd

users_data = {"id":[1,2,3,4 ], "name": ["Taariq", "Not Taariq", "Not Not Taariq", "Erik"]}
posts_data = {"id":[1,2,3], "body": ["Some post", "Some other post", "Some final post"], "user_id":[1,1,2]}

users = pd.DataFrame(users_data)
posts = pd.DataFrame(posts_data)
```

``` python
users.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|     | id  | name           |
|-----|-----|----------------|
| 0   | 1   | Taariq         |
| 1   | 2   | Not Taariq     |
| 2   | 3   | Not Not Taariq |
| 3   | 4   | Erik           |

</div>

``` python
posts.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|     | id  | body            | user_id |
|-----|-----|-----------------|---------|
| 0   | 1   | Some post       | 1       |
| 1   | 2   | Some other post | 1       |
| 2   | 3   | Some final post | 2       |

</div>

Lets join the tables

``` python
merged = posts.merge(users, left_on="user_id", right_on="id", how="inner", suffixes=("_post", "_user") )

merged.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|     | id_post | body            | user_id | id_user | name       |
|-----|---------|-----------------|---------|---------|------------|
| 0   | 1       | Some post       | 1       | 1       | Taariq     |
| 1   | 2       | Some other post | 1       | 1       | Taariq     |
| 2   | 3       | Some final post | 2       | 2       | Not Taariq |

</div>

# SQL

``` python
import sqlite3

connection = sqlite3.connect("./data/example.db")
cursor = connection.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);
""")

cursor.execute("""
CREATE TABLE IF NOT EXISTS posts (
    id INTEGER PRIMARY KEY,
    body TEXT NOT NULL,
    user_id INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
 )
"""
)
```

    <sqlite3.Cursor at 0x115081ec0>

FILL TABLES

``` python
users = [
    (1, "Taariq"),
    (2, "Not Taariq"),
    (3, "Not Not Taariq")
    ]

posts = [
    (1, "Some text", 1),
    (2, "Some text as well", 1),
    (3, "Some text that is nice", 2),
]

cursor.executemany(
"""
INSERT INTO users (id, name) values (?, ?)
""",
users
)

cursor.executemany(
"""
INSERT INTO posts (id, body, user_id) values (?, ?, ?)
""",
posts
)
```

    <sqlite3.Cursor at 0x115081ec0>

``` python
users_sql = cursor.execute("""
SELECT * 
FROM users as u
LEFT JOIN posts as p on u.id = p.user_id
""")

print(list(users_sql))
```

    [(1, 'Taariq', 1, 'Some text', 1), (1, 'Taariq', 2, 'Some text as well', 1), (2, 'Not Taariq', 3, 'Some text that is nice', 2), (3, 'Not Not Taariq', None, None, None)]

# RegEx

``` python
import re

text = "Hello, my name is taariq and my email is taariq.nazar97@math.su.se"
pattern = r"\b[\w.]+@[A-Za-z.]+\.[A-Za-z]{2,4}\b"
re.findall(pattern, text)
```

    ['taariq.nazar97@math.su.se']
