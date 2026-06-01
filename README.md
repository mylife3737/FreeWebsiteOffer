# Free Website Offer — Landing Page + Questionnaire

A 3-page static site. No build step, no dependencies to install — just HTML
(fonts load from Google Fonts over the web).

- `index.html` — the landing page (the "Free Website Design Giveaway" offer)
- `questionnaire.html` — the intake form the CTA button links to

## Launch it free on GitHub Pages

1. Create a new repository on GitHub (e.g. `free-website-offer`).
2. Upload these files to the repo root (`index.html`, `questionnaire.html`,
   and this `README.md`). You can drag-and-drop them in the GitHub web UI via
   **Add file → Upload files**, then **Commit changes**.
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set **Branch** to `main` and the folder to `/ (root)`, then **Save**.
6. Wait ~1 minute. Your site will be live at:
   `https://<your-username>.github.io/<repo-name>/`

The landing page loads first; clicking **Apply by June 4, 2026** opens the
questionnaire (`questionnaire.html`) in the same window.

## Custom domain (optional)

In **Settings → Pages → Custom domain**, enter your domain and follow the DNS
instructions GitHub shows. Add a `CNAME` file (GitHub creates it for you) and
point your domain's DNS to GitHub Pages.

## Collecting responses (Google Forms → Spreadsheet → email to you)

The questionnaire is already wired to submit to a Google Form. Once you plug in
your form's IDs, every submission lands in a Google Sheet and emails you.

> **Which account sends the emails:** automatic emails go out from whichever
> Gmail account owns the Form / Sheet / Apps Script. Do this whole setup while
> signed into **IsThisMyLife37@gmail.com** so that is the "from" address applicants
> and contacts see. Your own notification copies are BCC to
> **DianaLeff@gmail.com** (set in the script below). The winner / not-selected
> drafts also live in that sending account, so send those from there too.

### 1. Make the Google Form
1. Go to forms.google.com → blank form.
2. Add one **Short answer** question per field (names listed in the config block
   at the top of `questionnaire.html`): First name, Last name, Title, Email,
   Phone, Preferred contact, Business name, Business type, Online presence,
   Facebook, Instagram, Other social, Goal, Service area, Vibe, Inspiration,
   Logo status, Colors, Requirement 1, Requirement 2, Requirement 3, Notes,
   Submission Type.

### 2. Get the field IDs
1. In the form, click the **⋮** menu → **Get pre-filled link**.
2. Type a dummy value in every question → **Get link** → **Copy link**.
3. The link contains `entry.XXXXXXX` for each question. Match each to the keys
   in `GOOGLE_FORM_ENTRIES` inside `questionnaire.html`.
4. Replace `PASTE_YOUR_FORM_ID` in `GOOGLE_FORM_ACTION` with the ID from your
   form's edit URL: `docs.google.com/forms/d/e/THIS_PART/viewform`.

### 3. Spreadsheet of responses
In the form's **Responses** tab → **Link to Sheets**. Google creates a live
spreadsheet that fills in with every submission automatically.

### 4. Email yourself on each submission (and auto-confirm contacts)
In that spreadsheet: **Extensions → Apps Script**, paste this, save, then run
`createTrigger` once (approve the permissions prompt):

```js
function createTrigger() {
  ScriptApp.newTrigger('onSubmit')
    .forSpreadsheet(SpreadsheetApp.getActive())
    .onFormSubmit().create();
}

function onSubmit(e) {
  var v = e.namedValues;
  function get(name) { return (v[name] || [''])[0]; }
  var type = get('Submission Type');          // "Application" or "Contact only"
  var name = get('First Name') || get('Name');
  var email = get('Email');

  // 1) Notify you of every submission
  var body = '';
  for (var key in v) { body += key + ': ' + v[key] + '\n'; }
  MailApp.sendEmail('dianaleff@gmail.com',
    (type === 'Contact only' ? 'New contact message — ' : 'New free-website application — ') + name,
    body);

  // 2) If it's a contact message, auto-confirm to them within-24-hours promise
  if (type === 'Contact only' && email) {
    MailApp.sendEmail(email,
      "Thanks for reaching out — I'll reply within 24 hours",
      'Hi ' + name + ',\n\nThanks for reaching out about the free website offer. '
      + 'I have your question and will get back to you within 24 hours.\n\n'
      + 'Talk soon,\nDiana');
  }
}
```

From then on, every submission appears in the sheet AND lands in your inbox; the
contact messages also get an automatic confirmation reply.

## Contact form (the "Contact Me With Questions" button)

The contact form posts into the **same** Google Form and responses sheet as
applications — it just fills **Name → First Name**, **Email → Email**, **Message
→ Notes**, and sets **Submission Type = "Contact only"** so you can tell contact
messages apart (sort or filter the sheet by that column).

Nothing extra to set up: it already points at your main form's field IDs in the
`CONTACT_ENTRIES` block near the bottom of `index.html`. The combined Apps Script
above emails you for every submission and auto-sends contacts their 24-hour
confirmation.

*(You can trash the separate "Free Website Offer — Contact Messages" sheet in your
Drive — it's no longer used now that everything flows into one sheet.)*

## Notes

- The **logo file upload** can't travel through a Google Form. You'll collect the
  logo separately (ask for it in your follow-up email). why not??
