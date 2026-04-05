# Online Payment Integration Setup Guide
**For Public Donations & Admin Configuration**

This guide provides instructions on splitting the public payment portal and backend administration using modern payment gateways like Razorpay, ideal for Indian Temple Trusts.

## 1. Account Setup (Free Tier)
1. Register the Temple Trust on [Razorpay](https://razorpay.com/).
2. Submit Trust documents (Registration Certificate, PAN Card, Bank Details).
3. Switch to **Live Mode**.
4. Generate `Key ID` and `Key Secret` from Settings -> API Keys.

## 2. Public Interface (`harsidhdhi-mataji-temple-website.html`) Integration
Do NOT expose the `Key Secret` on the frontend HTML.

1. Include the Razorpay script in the `<head>` of the public site:
   `<script src="https://checkout.razorpay.com/v1/checkout.js"></script>`
2. Create a handler function:
```javascript
function processDonation(amount) {
    var options = {
        "key": "YOUR_RAZORPAY_KEY_ID", // Safe to expose public Key ID
        "amount": amount * 100, // Amount in paise
        "currency": "INR",
        "name": "Shri Harsidhdhi Mataji Trust",
        "description": "Temple Development Donation",
        "image": "temple_hero.png",
        "handler": function (response) {
            alert('Donation Successful! TXN ID: ' + response.razorpay_payment_id);
            // Optionally, call your backend API to register the donation
        },
        "theme": { "color": "#C9972A" }
    };
    var rzp1 = new Razorpay(options);
    rzp1.open();
}
```

## 3. Email Receipt Automation
To automatically send email receipts with the Harsidhdhi Temple branding:

1. Use **Razorpay Webhooks**. 
2. Set webhook URL to your backend endpoint (e.g., `https://your-server.com/webhook`).
3. Listen for the `payment.captured` event.
4. When triggered, use a service like **Nodemailer** or **SendGrid** in your backend to email the donor:
```javascript
// Example Backend Logic
if (event === 'payment.captured') {
    const amount = payload.payment.entity.amount / 100;
    const email = payload.payment.entity.email;
    sendReceiptEmail(email, amount); // Triggers Nodemailer
}
```

## 4. Admin Portal (`admin.html`) Management
Update the `panel-payments` section in `admin.html` to allow admins to rotate the Razorpay `Key ID` or update the Webhook forwarding email address dynamically via APIs connected to the PostgreSQL `livestream_config`/`settings` table.
