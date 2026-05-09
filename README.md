# Zihan Chen — Personal Academic Homepage

Personal academic homepage of Zihan Chen (陈子晗), built with Jekyll and the `jekyll-theme-minimal` theme, designed for GitHub Pages.

---

## How to edit content

1. Open `index.md` in any text editor.
2. Change the text — update your name, bio, education entries, experience entries, contact info, and the copyright year.
3. Commit and push to GitHub. GitHub Pages rebuilds the site within a minute.

You never need to touch HTML or CSS.

---

## How to change the profile photo

1. Replace `assets/img/zihan.jpg` with a new photo. Keep it roughly square for best results.
2. Keep the filename `zihan.jpg`, or update the `logo:` line in `_config.yml` to match the new filename.
3. Commit and push.

---

## How to add or change a university logo

1. Drop a PNG file into `assets/img/logos/` (e.g. `mit.png`).
2. In `index.md`, reference it with:

   ```html
   <img src="/assets/img/logos/mit.png" alt="MIT logo" height="40" align="left" hspace="10"/>
   ```

   Place this line directly above the institution heading. Add `<br clear="left"/>` after the bullet list for that institution to clear the float.

> **Note:** Real logos for UESTC, SUTD, NUS, and ZJU are already in `assets/img/logos/`. Add more the same way.

---

## How to enable GitHub Pages

1. Push this repository to a repo named `<your-username>.github.io` (for a user/org site) or any repo name (for a project site).
2. Go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**, select `main` (or `master`), and set the folder to `/ (root)`.
4. Click **Save**. Your site will be live at `https://<your-username>.github.io/` within a couple of minutes.

---

## Optional: previewing locally

If you have Ruby installed, create a `Gemfile` in the project root:

```ruby
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
```

Then run:

```bash
bundle install
bundle exec jekyll serve
```

Open `http://localhost:4000` in your browser. The `Gemfile.lock` is listed in `.gitignore` so it won't be committed.
