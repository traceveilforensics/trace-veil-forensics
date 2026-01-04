# EmailJS Setup Guide for Trace Veil Forensics

## Step 1: Create EmailJS Account

1. Go to: https://www.emailjs.com/
2. Click **"Sign Up"**
3. Sign up with **GitHub** or **Email**
4. Select **"Free"** plan

---

## Step 2: Create Email Service

1. In EmailJS Dashboard, click **"Email Services"** (left sidebar)
2. Click **"Add New Service"**
3. Choose **"Gmail"** or your email provider
4. Service Name: `trace-veil-notifications`
5. Click **"Create Service"**
6. Note your **Service ID** (looks like: `service_xxxxxxx`)

---

## Step 3: Create Email Template

1. Click **"Email Templates"** (left sidebar)
2. Click **"Create New Template"**
3. Choose **"Blank Template"**
4. Configure the template:

**Subject:**
```
New Inquiry - {{from_name}} - Trace Veil Forensics
```

**Body:**
```
You have a new contact form submission:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FROM: {{from_name}}
EMAIL: {{from_email}}
PHONE: {{phone}}
COMPANY: {{company}}
SERVICE: {{service}}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

MESSAGE:
{{message}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Sent from trace-veil-forensics.netlify.app
```

5. Click **"Save"**
6. Note your **Template ID** (looks like: `template_xxxxxxx`)

---

## Step 4: Get Public Key

1. Click **"Account"** (bottom left)
2. Find **"Public Key"** (looks like: `user_xxxxxxxxxxxxx`)
3. Copy it

---

## Step 5: Update contact.html

Edit `contact.html` and replace the placeholders:

**Line 12:**
```javascript
emailjs.init("YOUR_PUBLIC_KEY"); // Replace with your actual public key
```

**Line ~250 (in the send call):**
```javascript
await emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams);
```

Example:
```javascript
await emailjs.send('service_abc123', 'template_xyz789', templateParams);
```

---

## Step 6: Deploy Changes

```bash
cd "/home/felisaries/New Folder/Trace_Veil_Forensics"

git add contact.html
git commit -m "Add EmailJS configuration"
git push origin main
```

Netlify will auto-deploy!

---

## Step 7: Test

1. Go to: https://trace-veil-forensics.netlify.app/contact.html
2. Fill out the form
3. Click "Send Message"
4. Check `traceveilforensics@gmail.com` for the email

---

## Quick Reference

| Item | Where to Find |
|------|---------------|
| Public Key | Account → Profile |
| Service ID | Email Services → Your Service → Integration |
| Template ID | Email Templates → Your Template → Integration |

---

## Troubleshooting

**"Failed to send" error?**
- Check browser console (F12) for details
- Verify all IDs are correct in contact.html

**"Service not found"?**
- Verify Service ID is correct
- Make sure service is "Active" in EmailJS

**No email received?**
- Check spam folder
- Verify the template is saved
- Check EmailJS activity log

---

## Free Tier Limits

| Feature | Limit |
|---------|-------|
| Emails/month | 200 |
| Templates | 3 |
| Services | 2 |

More than enough for a small business website!

---

## Need Help?

- EmailJS Docs: https://www.emailjs.com/docs/
- Support: support@emailjs.com
