Code Review of Python Flask Web Application
Target Application: Simple user authentication system

Vulnerabilities Found:

SQL Injection

Raw SQL queries with string concatenation

Example: "SELECT * FROM users WHERE username = '" + username + "'"

Cross-Site Scripting (XSS)

User input rendered directly in HTML without escaping

Example: return "<div>Welcome " + username + "</div>"

Insecure Password Storage

Passwords stored in plaintext

No hashing or salting implemented

CSRF Protection Missing

No anti-CSRF tokens in forms

Sensitive Data Exposure

Debug mode enabled in production

Stack traces shown to users on errors

Secure Coding Recommendations:

SQL Injection Prevention

Use parameterized queries or ORM

Example: db.execute("SELECT * FROM users WHERE username = %s", (username,))

XSS Protection

Implement output encoding

Use template engines that auto-escape

Set Content Security Policy headers

Password Security

Implement bcrypt or PBKDF2 with proper salt

Example: bcrypt.hashpw(password.encode(), bcrypt.gensalt())

CSRF Protection

Add Flask-SeaSurf or implement CSRF tokens

Validate Origin/Referer headers

General Improvements

Disable debug mode in production

Implement proper error handling

Add security headers (HSTS, X-XSS-Protection)

Use prepared statements for all database access

Remediation Steps:

Replace all raw SQL with SQLAlchemy ORM

Implement Jinja2 templating with auto-escaping

Add password hashing using bcrypt

Integrate Flask-SeaSurf for CSRF protection

Configure production-ready settings

Tools Used:

Bandit (static analysis)

OWASP ZAP (dynamic analysis)

Manual code review

Documentation:

Created security findings report with risk ratings

Provided line-by-line remediation suggestions

Included references to OWASP Secure Coding Practices
