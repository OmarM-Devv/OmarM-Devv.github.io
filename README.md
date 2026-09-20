# Application Tracker Agent — website

The public site backing the Google OAuth consent screen for
[application-trakr](https://github.com/OmarM-Devv/application-trakr), a personal tool
that reconciles job-application activity from Gmail into a private Google Sheets
tracker.

It exists for one reason: Google will not move an External OAuth app from *Testing* to
*In production* without a homepage and a privacy policy on a verified domain. Leaving
the app in Testing expires the refresh token after seven days, which would make a
weekly scheduled job authenticate once and then go silently dead.

## Files

| File | Purpose |
|---|---|
| `index.html` | Homepage — what the tool does and which scopes it requests |
| `privacy.html` | Privacy policy, including Google's Limited Use declaration |
| `terms.html` | Terms of use |
| `style.css` | Shared styling |
| `.nojekyll` | Serves the files as-is, without Jekyll processing |

## Deployment

Served by GitHub Pages from `main` at <https://omarm-devv.github.io/>.

The repository must stay **public**: GitHub Pages on a private repository requires
GitHub Pro, and the tracker's own repository is private.

## Google OAuth fields

| Field | Value |
|---|---|
| App name | Application Tracker Agent |
| User support email | `umar2016mohamed@gmail.com` |
| App home page | `https://omarm-devv.github.io/` |
| Privacy policy | `https://omarm-devv.github.io/privacy.html` |
| Terms of service | `https://omarm-devv.github.io/terms.html` |
| Authorised domain | `omarm-devv.github.io` |

The authorised domain must first be verified in Google Search Console as a URL-prefix
property, using the HTML tag method — the meta tag lives in `index.html`.

## Keeping it honest

The scopes described here must match `src/tracker_agent/auth.py` in the tracker
repository. They are currently `gmail.readonly` and `spreadsheets`. If that list ever
changes, this site changes in the same commit — a privacy policy that misdescribes what
the code does is worse than none.

Never commit `credentials.json`, `token.json`, client secrets or refresh tokens here.
