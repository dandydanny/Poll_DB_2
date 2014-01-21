Poll_DB_2
=========

DBC Challenge 115









congress_members (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name VARCHAR(64) NOT NULL,
  party VARCHAR(64) NOT NULL,
  location VARCHAR(64) NOT NULL,
  grade_1996 REAL,
  grade_current REAL,
  years_in_congress INTEGER,
  dw1_score REAL
, created_at DATETIME, updated_at DATETIME);
voters (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    first_name VARCHAR(64) NOT NULL,
    last_name  VARCHAR(64) NOT NULL,
    gender VARCHAR(64) NOT NULL,
    party VARCHAR(64) NOT NULL,
    party_duration INTEGER,
    age INTEGER,
    married INTEGER,
    children_count INTEGER,
    homeowner INTEGER,
    employed INTEGER,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL
  );
votes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    voter_id INTEGER,
    politician_id INTEGER,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL,
    FOREIGN KEY(voter_id) REFERENCES voters(id),
    FOREIGN KEY(politician_id) REFERENCES congress_members(id)
  );


-------------


# Returns list of politicians, one from each state, sorted
# by the number of votes each state received. 
e.g.
id          name               party       location    COUNT(*)
----------  -----------------  ----------  ----------  ----------
216         Rep. Lynn Woolsey  D           CA          1025
457         Rep. Henry Cuella  D           TX          643
48          Sen. Chuck Schume  D           NY          582

SELECT congress_members.id, name, party, location, COUNT(*)
FROM congress_members
JOIN votes ON congress_members.id = votes.politician_id 
GROUP BY congress_members.location
ORDER BY COUNT(*) DESC
;




# Returns a list of all Texas politicians
SELECT congress_members.id, name, party, location
FROM congress_members
JOIN votes ON congress_members.id = votes.politician_id
WHERE location = 'TX'
;
