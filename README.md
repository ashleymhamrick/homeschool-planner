# Daybook: website

## Already done
- **Database (Supabase project "ashleymhamrick's Project", US West):** the `planners` and `photo_usage` tables, privacy rules so each family sees only their own planner, account deletion, and a monthly photo page count.
- **Photo reading:** the `read-photos` server function is live. It waits for your Anthropic key (below).
- **Invitations:** the `invite` server function is live. Only the owner email(s) in `ADMIN_EMAILS` can send invitations.
- **`config.js`:** filled in with this project's address and public key.

## Your steps (about 20 minutes)

### 1. Switch on photo reading
1. Go to console.anthropic.com and make a developer account. Add a few dollars of credit.
2. Make an API key. Do not send it to anyone, including Claude.
3. In Supabase, open **Edge Functions → Secrets** (or Project Settings → Edge Functions). Add a secret named `ANTHROPIC_API_KEY` and paste the key as its value.
4. Optional: add `PAGE_LIMIT` to change the photo pages each family gets per month (default 300).

### 2. Make the site invite-only
1. In Supabase, open **Authentication → Sign In / Providers** and turn off **Allow new users to sign up**. Invitations still work.
2. Add yourself: open **Authentication → Users → Add user → Send invitation** and type your email. Open the email on the device you'll use and follow the link.
3. Your owner email (ashleymhamrick@gmail.com) is already saved in the `site_admins` table. To add another owner later, add a row there in Supabase → Table Editor. The **Invite families** panel shows up only for owners.
4. To invite a family, type their email in **Invite families** and select **Send invitation**. They get an email with a link to make their planner.

### 3. Put the site online
Use GitHub Pages (free, public code) for testing, or Cloudflare Pages or Netlify to charge later. Upload `index.html`, `config.js`, and `privacy.html`.

### 4. Tell Supabase your site's address
In Supabase, open **Authentication → URL Configuration**. Set **Site URL** to the site's address, for example `https://yourname.github.io/homeschool-planner/`, and add the same address under **Redirect URLs**. Without this, sign-in links go to the wrong place.

### 5. Before many people sign up
Supabase's built-in email sender allows only a few emails an hour. Set up your own sender under **Authentication → Emails → SMTP Settings** (Resend, Postmark, or Amazon SES).

### 6. Fill in the privacy page
Replace the [bracketed] parts in `privacy.html` with your name, your contact email, and the date.

## Costs
- Supabase free plan: free projects pause after a week with no visits. Use Pro ($25/month) when families depend on it.
- Photo reading: about 1 to 2 cents a page, billed to your Anthropic account. The monthly page limit caps it per family.

## Files
| File | What it is |
| --- | --- |
| `index.html` | The site: sign-in, the welcome steps, and the planner |
| `config.js` | The project's address and public key |
| `privacy.html` | The privacy page (fill in the brackets) |
| `schema.sql` | The database setup, for your records (already applied) |
| `supabase/functions/read-photos/index.ts` | The photo-reading server function (already deployed) |
| `supabase/functions/invite/index.ts` | The invitation server function (already deployed) |
