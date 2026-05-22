---
sources:
  - https://developers.google.com/identity/sign-in/web/incremental-auth
publish: true
tags: [evergreen]
similar:
  - On Writing Software Well 4- Not every model is backed by a database (0.80)
  - Rewrite your Software (0.80)
  - Evergreen notes should fit on an index card (0.80)
  - Look for leverage (0.79)
  - architecture decisions (0.79)
---
An authorization style that Google encourages where you initially only request the minimal scopes from a user (ie name and email), then re-request more scopes as needed
