# Cattaraugus County Sales Explorer — by School District (Streamlit)

A variant of the Cattaraugus County Sales Explorer that profiles sales by **school district**
(`school_name`) instead of by municipality (`muni_name`). A school district can span more
than one municipality, so this gives a different slice of the same underlying data — useful
for questions tied to school funding or to a specific school's attendance zone rather than
town/village boundaries. Every filter, toggle, chart type, and the Total-row logic is
otherwise identical to the municipality version.

## Files

- `app.py` — the app itself
- `requirements.txt` — Python dependencies
- `cattco_sales_arms_length_Y_with_2026usd.csv` — the data file the app reads

## Run it locally

```bash
pip install -r requirements.txt
streamlit run app.py
```

It opens automatically in your browser (usually at `http://localhost:8501`). The app looks
for the CSV in the same folder as `app.py` by default; to point it somewhere else, set the
`CATTCO_DATA_PATH` environment variable to the file's full path before running.

## Deploy to Streamlit Community Cloud (free)

Same process as the municipality version:

1. **Create a GitHub repo** (a *different* repo from the municipality app, or a different
   folder/branch of the same one — Streamlit Community Cloud deploys one `app.py` per app)
   and push these three files to it.
2. Go to **[share.streamlit.io](https://share.streamlit.io)** and sign in with GitHub.
3. Click **"New app"**, select the repo/branch, and set `app.py` as the main file path.
4. Click **"Deploy"**. After the first build, the app is live at its own
   `<your-app-name>.streamlit.app` URL.
5. Push new commits any time to redeploy (e.g. a refreshed data file).

### A couple of things worth knowing

- **Cold starts**: an app with no recent visitors goes to sleep; the next visitor sees a
  short "waking up" delay before it's live again. Normal on the free tier.
- **Public repo = public code and data**: fine here, since this is public county
  sale-record data.
- Six records in the filtered sample have no `school_name` on file (vs. zero missing
  `muni_name`), so this app's county-wide totals differ very slightly from the municipality
  version's — by a handful of transactions, not a data error.

## Other hosting options

As a plain Streamlit app, this isn't locked to Streamlit Community Cloud — the same three
files can be deployed with a `Dockerfile` (`CMD streamlit run app.py --server.port=$PORT
--server.address=0.0.0.0`) to Render, Railway, Fly.io, a cloud VM, or similar.
