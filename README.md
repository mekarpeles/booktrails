# booktrails
A simple website for creating curriculum: directed sequences of books

# Concepts

If I've read "X", what can I then read next?

## UI

* v0 - linear lists (e.g. https://linkmix.co/en)
* v1 - DAGs, proposals / recommendations from others

## Schema

The db models and schema are being implemented on thebestbookon.com

`booktrails`

```
| id | title | username | created | updated |
```

`bookcrumbs`

```
| trail_id | openlibrary_work_id | previous_crumb (DEFAULT null) | 
```


```
class BookTrail(core.Base):
    __tablename__ = "booktrails"

    id = Column(BigInteger, primary_key=True)
    submitter = Column(Unicode, nullable=False) # e.g. @mekarpeles IA / Open Library username
    title = Column(Unicode, nullable=False)
    topic_id = Column(Integer, ForeignKey("topics.id")) # TBBO what?
    created = Column(DateTime(timezone=False), default=datetime.utcnow, nullable=False)
    modified = Column(DateTime(timezone=False), default=None)

class BookCrumb(core.Base):
    __tablename__ = "bookcrumbs"
    __table_args__ = (
        UniqueConstraint(
            'trail_id', 'work_id', 'previous_crumb', name='_crumb_uc'
        ),
    )
    id = Column(BigInteger, primary_key=True)
    trail_id = Column(Integer, ForeignKey("booktrails.id"))
    work_id = Column(Unicode, nullable=False) # Open Library work ID (required)
    # a trail could have multiple starting books & thus multiple crumbs with no previous_crumb
    previous_crumb = Column(Integer, ForeignKey("bookcrumbs.id"), default=None)
    comment = Column(Unicode, default=None)
    created = Column(DateTime(timezone=False), default=datetime.utcnow, nullable=False)
```

## Future Schema

These are all considered big distractions, keep it as absolutely as simple as possible for as long as possible.

* community tags
* upvotes
