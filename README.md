# VSSD Student Help Desk — one-time setup

A responsive student-support website prototype for Vikramajit Singh Sanatan Dharma College. It includes student signup/login, persistent PostgreSQL data via Supabase, complaint/query submissions, lost & found reports, event interest registrations, resource filters, announcements, admin publishing/status tools, an FAQ chatbot, and the student project credit for **Vaishnavi Singh · BCA First Year**.

## A. Connect the permanent database (required once)
1. Open https://supabase.com/ and create a project. Keep the database password private.
2. In the Supabase dashboard, go to **SQL Editor → New query**.
3. Open `supabase-schema.sql`, copy all contents, paste into the SQL Editor and click **Run**.
4. Open project **Settings → API** (or Connect/API keys). Copy the **Project URL** and the **anon/public key** (sometimes called publishable key). Never use the `service_role` key in frontend code.
5. Open `app.js` in VS Code and replace only `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE` and `PASTE_YOUR_SUPABASE_ANON_KEY_HERE` with your own values. Save.

## B. Run on your laptop (npm not required)
1. Extract the ZIP into a folder named `vssd-student-help-desk`.
2. Open VS Code → **File → Open Folder** → choose that folder.
3. Install the **Live Server** extension by Ritwick Dey if not already installed.
4. Right-click `index.html` → **Open with Live Server**. It opens an address like `http://127.0.0.1:5500`.
5. Refresh after editing `app.js`. The setup banner should disappear after both Supabase values are entered.

## C. Create your own admin account safely
1. Register through the website with an email you can access; confirm the email if Supabase requests it.
2. In Supabase SQL Editor run this, replacing the email with the exact email you registered:
   ```sql
   update public.profiles p set role='admin'
   from auth.users u where p.id=u.id and u.email='YOUR-EMAIL@example.com';
   ```
3. Log out and log back in. Open **My portal → Admin tools** to publish notices, add course-resource links, and update complaint statuses. The signup flow always assigns `student`; users cannot self-promote to admin.

## D. Publish a public website
1. Open https://www.netlify.com/ and create an account.
2. Choose manual deploy in the Netlify dashboard (label may change) and upload the extracted project folder contents — `index.html`, `styles.css`, `app.js`.
3. In Supabase Authentication URL settings, add your published Netlify URL to the allowed redirect URLs and set Site URL as needed.
4. Test the public URL on another browser/device and verify that test records persist after refresh.

## Honest scope and competition checklist
- Database records are persistent online while your Supabase project remains active. Notices/resources are not magically auto-updated: an authorised person must publish verified updates, or a separate approved integration must be built.
- Chatbot is a rule-based FAQ assistant, not an AI model.
- Department/course groupings are a starting directory, not a guarantee of current offerings. Verify exact current departments, course list, syllabus, holidays, staff and social URLs from official college sources before claiming them as official.
- Lost & found reports are private to the submitter and admins in this version. Public listing needs moderation and additional privacy design.
- This is a competition prototype, not a college-approved production system. Get college permission before using real student data. Use test accounts/data during judging; enable email confirmation and review security/backups before real deployment.
