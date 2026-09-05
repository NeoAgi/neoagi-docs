---
title: Login
description: Explains different types of logins and why they're needed.
---

Kept allows optionally logging into your NeoAgi Account it is completely optional functioning as 
a stand alone application to syncronize photos from your device to a supported storage provider.

While the NeoAgi Account login ***IS*** optional, connecting to a cloud storage provider may appear 
similar to a traditioinal login.  The goal of this guide is to outline the different types of login / 
authentication flows and what they do to provide visibility to what information is shared with NeoAgi.

## NeoAgi Account

Your NeoAgi Account can be accessed by logging in from the top right avatar in the application.

## Connector Login

Some connectors, like Google Drive and Microsoft OneDrive, are indpendent from the NeoAgi Account 
flows.  Although they look similarly as they're both OAuth Authuntication flows, they are intetionally 
separate to ensure that your NeoAgi Account doesn't implictly have access to your Google Drive data 
ensuring that only your device has access to your Google Drive data. 

We've designed our authentication flows to be the absolute minimum required to do the job at hand.  
For example, the Google Drive OAuth Grant's only the [https://developers.google.com/identity/protocols/oauth2/scopes#drive](https://www.googleapis.com/auth/drive.file) scope, limiting access to your Google Drive to only the files and folders Kept has 
created, never access to the full contents in the account.  

While connector logins may feel a bit redundant, we've done this in a way to meet two objectives:

1. To limit the access your NeoAgi Account has to your Cloud Resources to just that of your social profile (display name, email address, and related fields)
2. To allow cloud resources to be accessed without a NeoAgi Account

We've also tried to implement this in a way that minimizes how often you re-authenticate.  Hopefully 
it's only once at setup.

## Configuration Backup

An important call out for the backup and restore of configuration as it relates to logins.  

Authentication tokens stored on your device are ***not*** included in the backups.  While the backups 
are created on your device, transmitted to our backend systems over an enctypted channel, then 
encrypted before written to our secure storage.  We feel that omitting your authentication tokens 
in this process promotes a more secure posture by forcing you to re-authenticate with your provider 
after an import (only if the auth-token isn't already present on your device).