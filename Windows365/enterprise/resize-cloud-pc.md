---
# required metadata
title: Resize a Cloud PC
titleSuffix:
description: Learn how to resize a Cloud PC by using Microsoft Intune.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/28/2025
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Cloud PC resizing overview

[!INCLUDE [Resize a Cloud PC intro](../includes/resize-introduction.md)]

Downsizing may impact support for nested virtualization. For more information, see [Set up virtualization-based workloads support](nested-virtualization.md).

## Resizing details

> [!IMPORTANT]
> Before triggering a resize for Windows 365 Enterprise Cloud PCs, ensure that you are following best license assignment practices. Resizing Cloud PCs is simpler when using discrete Entra groups for licensing that are different from the Entra groups used for provisioning policy targeting. For more information, follow [Provisioning in Windows 365 | Microsoft Learn](/windows-365/enterprise/provisioning)

For Windows 365 Enterprise, the Cloud PC size is tied to the license assigned to its user. When resizing Cloud PCs that have been provisioned with direct assigned licenses, the Windows 365 service will do the license reassignment on behalf of the admin. When resizing Cloud PCs that have been provisioned with group-based licenses (assigned through Entra group membership), the Cloud PC will enter the **Resize pending license** state. Once in this state, the admin needs to assign the appropriate target license to trigger the resize. 

The **Resize pending license** state:

- has a duration of 48 hours. If the original license is removed but the new license isn't assigned within 48 hours, the device goes into a [grace period](device-management-overview.md).
- If the wrong target license is chosen, the Cloud PC is provisioned matching the configuration of that wrong license.

- If the source license isn't removed first, and the new license is assigned to the user, the new license is used to resize the current Cloud PC. In addition, the original license is used to provision another, new Cloud PC for the user.

- If the source license isn't removed, and the target license isn't assigned within 48 hours, the device returns to the **Provisioned** state.

If you have a combination of paid and trial licenses, the resize feature uses your paid licenses first. After these licenses run out, the resize operation uses your trial licenses.

[!INCLUDE [Resize a Cloud PC details](../includes/resize-details.md)]

## Resize with Step-up Licenses

The Windows 365 step-up licenses are lead status licenses available for Enterprise admins that have a direct Enterprise Agreement. A step-up SKU makes it easier for admins to migrate users from a lower-configuration license to a higher-configuration license without incurring the full cost of licensing two separate subscriptions of the product. For Windows 365, step-ups are available for compute (RAM/CPU) and storage and scoped to upgrades and not downgrades of licenses.

If you converted a Windows 365 Enterprise license subscription by purchasing Microsoft Step-up Licenses, you can migrate your users to the new license and preserve all user data by performing a bulk resize for those users.  

For example, let's say that you used a Step-up purchase to convert licenses from a Windows 365 Enterprise 2vCPU/4 GB/128 GB subscription to a Windows 365 Enterprise 4vCPU/16GB/128 GB subscription. In this case, follow the steps under [Bulk resize Cloud PCs originally provisioned with group-based licenses](resize-cloud-pc-bulk.md#bulk-resize-cloud-pcs-originally-provisioned-with-group-based-licenses). The Windows 365 2vCPU, 4 GB, 128 GB is your base license, and the Windows 365 4vCPU/16GB/128 GB is your target license.  

When a Step-up conversion takes place, the stepped-up licenses show up in your inventory equaling the number of old licenses you chose to convert. If you Step-up 10 licenses of Windows 365 Enterprise 2vCPU/4GB/128 GB to 4vCPU/16 GB/128 GB, you end up with 10 more licenses of 4vCPU/16 GB/128 GB and 10 fewer licenses of 2vCPU/4GB/128 GB. These changes appear on the **Your Products** page in the Microsoft admin center.

When you step up a license subscription, you must make sure that you're ready to migrate or resize the users to the new license subscription that you're stepping up to. If you step up all licenses within your subscription, you have 90 days to migrate your users to the new licenses before they lose access to the Cloud PC provisioned with the original license. However, if you only step up a subset of licenses within a subscription, you must migrate your users immediately to avoid any service disruption. To ensure uninterrupted access for your users, plan the migration of your users promptly after purchasing step-up licenses.

## Resize after upgrading licenses purchased through a Microsoft Customer Agreement

If you have a Microsoft Customer Agreement (MCA), you can upgrade your license as explained in [Upgrade or change to a different Microsoft 365 for business plan](/microsoft-365/commerce/subscriptions/upgrade-to-different-plan). After upgrading, you can resize Cloud PCs as explained in this article.

## Resize a Cloud PC flow diagram

:::image type="content" alt-text="Flowchart of actions for an admin to resize a Cloud PC." source="./media/resize-cloud-pc/resize-cloud-pc-diagram.png":::

<!-- ########################## -->
## Next steps

[Resize a single Cloud PC](resize-cloud-pc-single.md).

[Resize multiple Cloud PCs in bulk](resize-cloud-pc-bulk.md).

For more information on Cloud PC sizes, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).
