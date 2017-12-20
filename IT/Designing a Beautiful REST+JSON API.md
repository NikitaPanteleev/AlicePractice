http://www.youtube.com/watch?v=5WXYw4J4QOU&list=PL6yAo1YfMf8J4-buSxQ87lxi9FBWr2n7P

# Resources
Collection Resource -> /applications
Instance Resource   -> /applications/a1b2c3
# Behavior
 - GET = read
 - POST \
 - PUT -- add and update
 - DELETE
 - HEAD = header, no body

PUT must be idempoten. No matter how many times i call it, the result
is the same.
# Media-Types
Represent the version in media-types.

#CamelCase
Stay consistent. Properties and function names are unconventional fo
JS. Stay consistent.
#Date/Time
ISO 8601
# HREF
Every accessible Resource has a unique URL. Use complete URL in
linking objects:
```
"media" : "http://api.toprater.com/v1/images/axfddd8f.jpg"
```
# Response body
Return (by default) if feasible the representation.

# Content negotiation
Header values comma delimited in order for preference. Or resource
extensions /applications/aax3.csv or /applications/aax3.csv
