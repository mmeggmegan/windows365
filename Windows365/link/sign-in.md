---
# required metadata
title: Sign in to your Windows 365 Link
titleSuffix:
description: Learn how to sign in, sign our, and lock your Windows 365 Link
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/16/2025
ms.topic: overview
ms.service: windows-365-link
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Sign in to, sign out, or lock your Windows 365 Link

When you want to use the Windows 365 Link, complete the following steps to sign in:

1. Power on the Windows 365 Link.
2. On the **Sign in** screen, provide your sign in credentials. The device automatically presents you with the sign-in process configured by your organization (FIDO2 security key, Passkey (FIDO2), Microsoft Authenticator app, and so on).
3. Authenticate your account as requested.
4. You're connected to your Cloud PC.

## Sign out

To sign out of your Windows 365 Link:

- Press control-alt-delete and select **Sign out**, or
- Select Start > your account > **Sign out**.

Signing out disconnects the current signed in user from their Cloud PC and brings Windows 365 Link back to the sign-in screen.

## Lock your Windows 365 Link

Lock the device using any of these methods:

- Press the **Windows key + L** on your keyboard.
- Press control-alt-delete and select **Lock**.

After the user locks the device, the user is redirected back to the **Sign in** screen.

If Windows 365 Link is locked, the current signed in user’s connection to their Cloud PC is maintained until Cloud PC’s idle time-out expires. Intune admins can configure the time-out duration, which defaults to 15 minutes. Within this time window, if the user unlocks Windows 365 Link by completing the authentication experience again, they're taken directly on their Cloud PC without the need for re-establishing the connection.

If a new user signs into the device during this time, the previous user’s Cloud PC connection is disconnected and a new connection is established from the device to the new user’s Cloud PC.

## Disconnect Windows 365 Link from your Cloud PC

You can disconnect the device from your Cloud PC using any of these methods:

- Press control-alt-delete and select **Sign out**.
- In your Cloud PC, select Start > **Power** > **Disconnect**.
- In your Cloud PC, select Start > **Power** > **Lock**.\*

\* This method locks the remote session on the Cloud PC. Single sign-on connections are also disconnected (but admins can configure policies to behave differently). Disconnecting from the Cloud PC brings the Windows 365 Link back to the sign-in screen.

## Data

Your data and account information aren't stored on the Windows 365 Link. If someone else signs into their account on the Windows 365 Link, the previous user's Cloud PC connection is automatically disconnected and the new user has no access to the previous user's data.

## Connection Center

If a user is assigned more than one Windows 365 Cloud PC, the Connection Center screen appears when a user first signs in to their Windows 365 Link device and on the Control Alt Delete screen. On the Connection Center screen, users can:

- Choose which of their Cloud PCs to connect to.
- Troubleshoot connection errors.
- Reboot and restore their Cloud PCs.

<!-- ########################## -->
## Next steps

[Use Quick Settings to view and manage monitors, languages, network connections, and more](quick-settings.md).

[Use the Control-Alt-Delete menu manage tasks, connections, sign-out, or lock your Windows 365 Link.](control-alt-delete.md)
