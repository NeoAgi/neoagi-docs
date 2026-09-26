---
title: Kept
description: How Kept handles your files, permissions, and privacy across Google Drive, OneDrive, and WebDAV.
sidebar:
  label: Overview
---

Kept backs up your photos and files to a cloud storage provider you choose: Google Drive,
OneDrive, or your own WebDAV server. This page covers what Kept can and can't see, what it does
with your credentials, and what (if anything) leaves your device besides the files you're
backing up.

## Storage Providers

### Google Drive

When you connect Google Drive, Kept requests a Google API permission called `drive.file` rather
than full Drive access. Under this permission, Google's servers will only return files and
folders that Kept itself created.  The rest of your Drive is invisible to the app at the API
level. It isn't a setting Kept could choose to ignore; Google's API simply doesn't hand back
anything else.

In practice this means when you pick a backup destination inside Kept, you'll only ever see
folders Kept made. Your existing Google Drive folders won't show up in that picker.  Not because
Kept is hiding them, but because it has no way to see them at all.

### Microsoft OneDrive

OneDrive's connection asks for broader access (`Files.ReadWrite`) than Google Drive's does,
because Microsoft's narrower app-scoped permission would have locked backups to a single fixed
folder Kept couldn't let you choose. So for OneDrive, "Kept only touches the backup folder you
picked and nothing else" is a promise Kept's own code keeps, not one enforced by Microsoft's API
the way it is with Google. We think that's still worth knowing, not just worth stating.

### NAS over WebDav

WebDAV connections sign in directly to a server you provide, typically a home NAS, using a
username and password, not an OAuth grant. There's no vendor-side scoping concept here at all;
Kept's behavior on your server is governed entirely by the app's own code and by whatever
permissions your server account has.

If your server uses a self-signed certificate, Kept offers an explicit "skip TLS verification"
toggle. It's off by default, and it's meant only for self-signed certs on networks you trust —
turning it on means Kept will accept any certificate your server presents, so leave it off unless
you know you need it.

## Kept Does Not Delete Files

Across all three providers, Kept's sync engine has no delete capability at all.  The code path
that talks to Google Drive, OneDrive, and WebDAV servers can create folders and upload files, and
nothing else. There's no setting to turn this off because there's nothing to turn off: removing a
file from your device or from your cloud storage isn't something Kept's sync engine can do.

## Credential Storage

Google and OneDrive sign-in tokens, and WebDAV passwords, are stored using your device's secure
credential storage (the iOS Keychain or Android Keystore); the same system iOS and Android use
to protect passwords for other apps. Kept's own local database, which tracks things like
connection names and sync status, never stores a token or password field at all.

## Photo Library Access

On iOS, if you choose "Limited Access" when granting Kept your photo library permission, Kept
backs up only the photos you've selected.  It doesn't ask again or try to work around that
choice. Kept will suggest Full Access so nothing gets missed, but Limited Access is fully
supported.

On Android, Kept asks for permission to your photos and videos specifically (rather than the
broader storage permission older Android apps used), so it can't see other apps' documents or
downloads.

## What Kept Shares

Kept sends anonymous usage metrics, counts like how many files were uploaded, how many bytes,
and whether a sync succeeded, to help us understand reliability. These metrics never include
filenames, file paths, file contents, or references to your device, account, or identifyable information.

Separately, Kept keeps an on-device diagnostic log that can include filenames (for example, to
record which file failed to upload and why). That log stays on your device and is never sent
anywhere automatically.  It's only shared if you go to Diagnostics and explicitly choose to send
it to support... displaying exactly what would be sent and only after confirming a dialog stating the 
informaiton will be sent and even then only under a randomly generated support token that you must 
provide to us to connect the logs to your account that changes with every press and contains no device 
information.  
