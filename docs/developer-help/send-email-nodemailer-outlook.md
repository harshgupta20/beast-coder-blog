---
sidebar_position: 6
title: "Send Email - Nodemailer"
---

# Send Email with Nodemailer Using Microsoft Outlook in Node.js

Sending emails from a Node.js application is a common requirement, especially for sending notifications, reports, or automated messages. In this guide, I'll walk you through setting up Nodemailer to send emails using Microsoft Outlook.

## Prerequisites

Before we start, make sure you have the following:

- Node.js installed on your machine.
- An Outlook email account with the correct credentials.
- Basic knowledge of Node.js and its ecosystem.

## Step 1: Set Up Your Node.js Project

Let's create a new Node.js project if you don't have one already.

```bash
mkdir nodemailer-outlook
cd nodemailer-outlook
npm init -y
```


## Step 2: Install Nodemailer

Next, let's install Nodemailer, which we'll use to send emails.

```bash
npm install nodemailer
```
Nodemailer will now be part of your Node.js project.


## Step 3: Configure Nodemailer to Use Outlook SMTP
Nodemailer uses SMTP (Simple Mail Transfer Protocol) to send emails. To connect to Outlook's SMTP server, you need to set up a transporter with the correct configuration.

Here's a simple code snippet to create a Nodemailer transporter for Outlook:

```bash
const nodemailer = require('nodemailer');

const transporter = nodemailer.createTransport({
  host: 'smtp.office365.com',
  port: 587, // Use 587 for Outlook
  secure: false, // true for 465, false for other ports
  auth: {
    user: 'your_email@outlook.com', // Your Outlook email
    pass: 'your_password' // Your Outlook password
  }
});
```
Replace 'your_email@outlook.com' and 'your_password' with your Outlook email and password.


## Step 4: Create a Function to Send Email
ow let's create a function that sends an email. This function will take some basic parameters like to (recipient), subject, and html (email content).

Here's a simple code snippet to create a Nodemailer transporter for Outlook:

```bash
async function sendEmail(to, subject, html) {
  try {
    const mailOptions = {
      from: 'your_email@outlook.com', // Your Outlook email
      to: to, // Recipient
      subject: subject, // Subject of the email
      html: html // HTML content of the email
    };

    const info = await transporter.sendMail(mailOptions);
    console.log('Email sent: ' + info.response);
  } catch (error) {
    console.error('Error sending email:', error);
  }
}
```


## Step 5: Test the Email Function
With the 'sendEmail' function ready, let's test it by sending a simple email with some HTML content.

Here's a simple code snippet to create a Nodemailer transporter for Outlook:

```bash
sendEmail('recipient@example.com', 'Test Email', '<h1>Hello World!</h1><p>This is a test email.</p>');
```
Replace 'recipient@example.com' with the email address to which you want to send the email.


## Bonus Section: Sending Emails with Attachments and CC
Nodemailer allows you to send emails with attachments and CC (carbon copy). Let's modify our "sendEmail" function to include these features.

```bash
const path = require('path');

async function sendEmailWithAttachment(to, cc, subject, htmlContent, attachmentFilename) {
  try {
    const attachmentPath = path.resolve(__dirname, attachmentFilename); // Construct the absolute path to the attachment

    const mailOptions = {
      from: 'your_email@outlook.com',
      to: to,
      cc: cc,
      subject: subject,
      html: htmlContent,
      attachments: [
        {
          filename: attachmentFilename,
          path: attachmentPath
        }
      ]
    };

    const info = await transporter.sendMail(mailOptions);
    console.log('Email with attachment sent: ' + info.response);
  } catch (error) {
    console.error('Error sending email with attachment:', error);
  }
}
```
This modified function allows you to send emails with attachments and CC. Note that we use the "path" module to ensure that we can locate the attachment file correctly.

## Conclusion 🎉
That's it! You've learned how to send emails from a Node.js application using Nodemailer and Microsoft Outlook. This guide showed you how to set up a basic transporter, send simple emails, and include attachments and CC recipients. You can expand on this to create more complex email functionality or integrate it into your Node.js applications.

Happy coding! If you have any questions, feel free to ask in the comments, and I'll be happy to help.