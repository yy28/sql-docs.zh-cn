---
title: Azure 存储连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8a115dafb386323bc1f4738720e7576657d22543
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316689"
---
# <a name="azure-storage-connection-manager"></a>Azure 存储连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  通过 Azure 存储连接管理器，SSIS 包可与 Azure 存储帐户进行连接  。
   
 Azure 存储连接管理器是[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的一个组件  。 
  
在“添加 SSIS 连接管理器”  对话框中，选择“AzureStorage”  ，然后单击“添加”  。  
  
可使用以下属性。

- **服务：** 指定要连接到的存储服务。
- **帐户名：** 指定存储帐户名。
- **身份验证：** 指定要使用的身份验证方法。 支持 AccessKey 和 ServicePrincipal 身份验证   。
    - **AccessKey：** 指定此身份验证方法的帐户密钥  。
    - **ServicePrincipal：** 对于此身份验证方法，请指定服务主体的应用程序 ID、应用程序密钥和租户 ID    。
      要使“测试连接”起作用，应向服务主体分配至少存储帐户的“存储 Blob 数据读取器”角色   。
      请参阅[此](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal)页获取详细信息。
- **环境：** 指定托管存储帐户的云环境。
