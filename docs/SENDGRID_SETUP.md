# SendGrid Email Setup - Quick Start

## ✅ What We Have
- SendGrid API Key: `SG.GSILKJNS.YSKHS_YEU`
- Email service code: Updated and ready

## ❗ What We Need from Client

### 1. Verify Sender Email Address

**The client MUST complete this step before emails will work:**

The sender email address needs to be verified in the SendGrid account. Please ask the client to:

1. Log in to [SendGrid Dashboard](https://app.sendgrid.com/)
2. Navigate to **Settings → Sender Authentication**
3. Click **"Verify a Single Sender"**
4. Fill in the form:
   - **From Email Address:** `noreply@bellacarwash.co.uk` (or their preferred email)
   - **From Name:** Bella Car Wash
   - **Reply To:** info@bellacarwash.co.uk
   - **Company Address:** (their business address)
5. Submit and check email for verification link
6. Click the verification link in the email

**⏱️ This takes about 5 minutes to complete.**

### 2. Confirm Verified Email

Once verified, the client should tell us which email address was verified. We'll use that in our configuration:

```env
SENDGRID_FROM_EMAIL=noreply@bellacarwash.co.uk
```

If they verified a different email (like `info@bellacarwash.co.uk`), we'll use that instead.

## 🚀 Deployment Steps

### Step 1: Set Environment Variables on Railway

```bash
# Set SendGrid API Key
railway variables set SENDGRID_API_KEY=SG.GSILKJNS.YSKHS_YEU

# Set verified sender email (update with actual verified email from client)
railway variables set SENDGRID_FROM_EMAIL=noreply@bellacarwash.co.uk

# Set frontend URL for email links
railway variables set FRONTEND_URL=https://your-vercel-url.vercel.app
```

### Step 2: Deploy Backend

```bash
cd backend
railway up
```

### Step 3: Test Email Sending

After deployment, test by:
1. Going to admin panel
2. Approving or rejecting a partner application
3. Check SendGrid Dashboard → Activity Feed for email delivery status

## 📧 Email Templates Configured

### 1. Partner Approval Email
- Sent when admin approves partner application
- Includes: Welcome message, location count, dashboard link

### 2. Partner Rejection Email
- Sent when admin rejects partner application
- Includes: Polite message, optional reason, contact support link

## 🔍 Monitoring & Testing

### Check Email Delivery in SendGrid

1. Go to [SendGrid Dashboard](https://app.sendgrid.com/)
2. Click **Activity Feed** in left menu
3. See all sent emails with status:
   - ✅ **Delivered** - Email successfully sent
   - ⏳ **Processed** - Email in queue
   - ❌ **Bounced** - Email address invalid
   - 🚫 **Blocked** - Spam filter caught it

### View Email Analytics

SendGrid provides detailed analytics:
- **Opens:** How many recipients opened the email
- **Clicks:** Link clicks in emails
- **Bounces:** Invalid email addresses
- **Spam Reports:** Recipients marked as spam

Access at: Dashboard → Statistics

## 📋 Message for Client

**Email Template:**

---

Hi [Client Name],

To enable email notifications for partner approvals/rejections, we need you to verify the sender email address in your SendGrid account. This is a quick 5-minute process:

**Steps:**
1. Log in to https://app.sendgrid.com/
2. Go to Settings → Sender Authentication
3. Click "Verify a Single Sender"
4. Use email: **noreply@bellacarwash.co.uk**
5. Fill in your company details
6. Check your email and click the verification link

Once verified, please confirm and we'll deploy the email functionality immediately.

**Alternative:** If you prefer to use a different email address (like info@bellacarwash.co.uk), just let us know which one you verified.

Thanks!

---

## 🆘 Support & Troubleshooting

### If Emails Don't Send

1. **Check Railway Logs:**
   ```bash
   railway logs
   ```
   Look for: `✅ Email sent successfully` or `❌ Failed to send email`

2. **Check Environment Variables:**
   ```bash
   railway variables
   ```
   Verify `SENDGRID_API_KEY` and `SENDGRID_FROM_EMAIL` are set

3. **Verify Sender in SendGrid:**
   - Settings → Sender Authentication
   - Look for green checkmark next to email address

4. **Check API Key Permissions:**
   - Settings → API Keys
   - Ensure key has "Mail Send" permission (Full Access recommended)

### SendGrid Free Tier Limits

- **100 emails per day**
- Sufficient for MVP testing
- If exceeding, client needs to upgrade plan

### Upgrading SendGrid Plan

If higher email volume needed:
- Essentials: $15/month for 40,000 emails
- Pro: $90/month for 100,000 emails

## ✅ Checklist Before Going Live

- [ ] Client verified sender email in SendGrid
- [ ] Client confirmed which email address was verified
- [ ] `SENDGRID_API_KEY` set on Railway
- [ ] `SENDGRID_FROM_EMAIL` set on Railway (matches verified email)
- [ ] `FRONTEND_URL` set on Railway (for email links)
- [ ] Backend deployed to Railway
- [ ] Test email sent successfully (check Activity Feed)
- [ ] Email received in inbox (not spam)

## 📞 Next Steps

1. **Send verification request to client** (use email template above)
2. **Wait for confirmation** that email is verified
3. **Update `SENDGRID_FROM_EMAIL`** environment variable if needed
4. **Deploy to Railway** with environment variables
5. **Test with real partner approval** to confirm working

---

**Current Status:** ⏳ Waiting for client to verify sender email address

**ETA:** 5 minutes after client completes verification
