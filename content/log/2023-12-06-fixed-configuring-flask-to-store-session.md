<!-- title: Fixed: Configuring Flask to Store Session -->
<!-- summary: Note to self: sometimes error messages are hidden in tooltips. -->

The Win: 
- Got session cookie to save in browser during login function

The Problem: 
- Had been working fine (session cookie visible upon POST to `/login`) in Postman
  - But cookie wasn't showing up in browser at all

Error messages:   
- Warning symbol in dev tools Network panel, next to `Set-Cookie` response header
- Hover over the warning, don't click it! Error message in tooltip (facepalm)
- Message said `Set-Cookie` header attributes needed to include `SameSite=None` and `Secure`
  - (Incorrect) value of `Set-Cookie` header:               `session=eyJ1c2VyX2lkIjo1N30.ZXE6sg.EsJhvTt1JwLLKYaAHhGb6H5WXxY; HttpOnly; Path=/;`
  - `SameSite` defaulted to "Lax"

The Solution:
- Add configuration to `app.py` like so:
```py
    app.config['SESSION_COOKIE_SAMESITE'] = "None"
    app.config['SESSION_COOKIE_SECURE'] = True

    # Note that "None" is a string, not the datatype None
```
