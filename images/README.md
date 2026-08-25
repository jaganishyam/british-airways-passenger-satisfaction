# Dashboard screenshots

This folder is where dashboard exports go. **Adding them is the single highest-value improvement you
can make to this repo** — GitHub renders images inline in the README, and a recruiter who sees a
dashboard in the first three seconds is far more likely to keep reading than one who has to download
a `.twbx` and install Tableau.

## Export steps (about two minutes)

In Tableau Desktop, open each dashboard and use **Dashboard → Export Image…** (PNG):

| Save as | From |
|---|---|
| `dashboard-1-executive-overview.png` | Dashboard 1 – Executive Overview |
| `dashboard-2-service-quality.png` | Dashboard 2 – Service Quality |
| `dashboard-3-geography-aircraft.png` | Dashboard 3 – Geography & Aircraft Performance |

Then delete this file and add the images to the main `README.md`, just under the Dashboards table:

```markdown
### Dashboard 1 — Executive Overview
![Executive Overview](images/dashboard-1-executive-overview.png)

### Dashboard 2 — Service Quality
![Service Quality](images/dashboard-2-service-quality.png)

### Dashboard 3 — Geography & Aircraft Performance
![Geography and Aircraft](images/dashboard-3-geography-aircraft.png)
```

Keep each PNG under about 1 MB so the README loads quickly.
