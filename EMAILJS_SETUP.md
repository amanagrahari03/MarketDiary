# EmailJS Setup Guide

## Steps to Set Up Email Support

### 1. Go to EmailJS Website

- Visit https://www.emailjs.com/
- Click "Sign Up Free"
- Create an account (use your email)

### 2. Create Email Service

- After login, go to **Email Services** (left sidebar)
- Click **"Add Service"**
- Choose **Gmail** (or your preferred email provider)
- Click **"Connect Account"** and authorize with your Gmail account (amanagrahari1433@gmail.com)
- Set Service ID (e.g., `service_marketdiary`) - **copy this**

### 3. Create Email Template

- Go to **Email Templates** (left sidebar)
- Click **"Create New Template"**
- Name it `support_template`
- Use this template code:

```
Subject: Support Request from {{from_name}}

From: {{from_name}} ({{from_email}})
Subject: {{subject}}

Message:
{{message}}

---
Reply to: {{from_email}}
```

- Click **Save**
- Copy the **Template ID** (e.g., `template_xxxxx`)

### 4. Get Your Public Key

- Go to **Account** (top right)
- Click **API Keys**
- Copy your **Public Key** (NOT Private Key)

### 5. Update HelpSupportModal.jsx

Replace these three values in `src/components/HelpSupportModal.jsx`:

```javascript
emailjs.init("YOUR_PUBLIC_KEY_HERE"); // Line 7

// In handleSubmit(), replace these (around line 45):
await emailjs.send(
  "service_marketdiary", // Your Service ID
  "support_template", // Your Template ID
  {
    to_email: "amanagrahari1433@gmail.com",
    from_name: formData.name,
    from_email: formData.email,
    subject: formData.subject,
    message: formData.message,
  }
);
```

### Example Values:

- Public Key: `z1a2b3c4d5e6f7g8h9i0j`
- Service ID: `service_marketdiary`
- Template ID: `template_abcdef`

### 6. Test

- Run your app: `npm run dev`
- Click "Help & Support" in footer
- Fill in and send a test message
- Check your email (amanagrahari1433@gmail.com) for the message
- User won't see your email address in the modal

## Security Notes

✓ User's email is captured but NOT displayed
✓ Your email (amanagrahari1433@gmail.com) only appears on backend
✓ Public Key is safe to expose in frontend code
✓ EmailJS is free for up to 200 emails/month
