---
title: Mail Configuration
description: Configure the mail server to send emails from Wiki.js
published: true
date: '2026-08-20T07:07:21.376Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-11T05:45:43.835Z'
---

You must configure the access to a mail server in order to receive emails from Wiki.js. This is required to send important emails like password resets, welcome emails, notifications, etc.

# Configuration

| Parameter | Description |
| :------- | :------- |
| **Sender Name** | Name of the sender for all outgoing emails. |
| **Sender Email** | Email address of the sender for all outgoing emails. | 

# SMTP Settings

| Parameter | Description |
| :-- | :-- |
| Host | Hostname or IP address of the SMTP mail server. |
| Port | Port of the SMTP mail server. Usually `465`, `587` or `25`. |
| Client Identifying Name | An optional name to send to the SMTP server to identify your mailer. Leave empty to use server hostname. For Google Workspace customers, this should be your main domain name. |
| Secure (TLS) | Should be enabled when using port `465`, otherwise turned off (`587` or `25`). |
| Verify SSL Certificate | Some hosts requires SSL certificate checking to be disabled. Leave enabled for proper security. |
| Username | Username used for authenticating to the SMTP server. |
| Password | Password used for authenticating to the SMTP server. |
{.table-leading-col}

# DKIM

DKIM (DomainKeys Identified Mail) provides a layer of security on all emails sent from Wiki.js by providing the means for recipients to validate the domain name and ensure the message authenticity. Note that not all mail providers offer support for this feature.

To enable DKIM, enable the toggle for **Use DKIM**. Additional configuration options will appear below.

| Parameter | Description |
| :-- | :-- |
| Domain Name | Domain name used for DKIM validation. |
| Key Selector | Determines which key to use for DKIM in your DNS records.‍ |
| Private Key | ‍Private key for the selector in PEM format. |
{.table-leading-col}

# Mail Templates

*Coming soon*

# Send a Test Email

Make sure to apply any changes to the mail configuration before attempting to send a test email!

Enter the recipient email address and click **Send Email**. A test email will be sent to the provided email address using the mail server settings you entered.
