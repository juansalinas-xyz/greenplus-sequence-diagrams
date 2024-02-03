sequenceDiagram
participant p as Person
participant f as front
participant b as backend
participant db as Mongo

p-->>+f: GET/Home
f-->>-p: return ok
p-->>+f: GET: /market
    f-->>+b: GET /market
    note over f,b: query: from,to
        b-->>+db: search
        note over b,db: where order in (from,to)
        db-->-b: return Projects
    b-->-f: Projects
f-->-p: return Projects