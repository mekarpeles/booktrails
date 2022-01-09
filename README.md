# booktrails
A simple website for creating curriculum: directed sequences of books

## UI

* v0 - linear lists (e.g. https://linkmix.co/en)
* v1 - DAGs

## Schema

`booktrails`

```
| id | title | username | created | updated |
```

`bookcrumbs`

```
| trail_id | openlibrary_work_id | previous_crumb (DEFAULT null) | 
```

## Future Schema

These are all considered big distractions, keep it as absolutely as simple as possible for as long as possible.

* community tags
* upvotes
