---
title: "Azure 资源管理器连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd1dbf668bf3ac24d9d6598b0ff9e2256d897c42
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-resource-manager-connection-manager"></a>Azure 资源管理器连接管理器
**Azure 资源管理器连接管理器**允许 SSIS 包来管理 Azure 资源使用[服务主体](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)。

**Azure 资源管理器连接管理器**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

若要创建和配置**Azure 资源管理器连接管理器**，按照以下步骤：

1. 在**添加 SSIS 连接管理器**对话框中，选择**AzureResourceManager**，然后单击**添加**。
2. 在**Azure 资源管理器连接管理器编辑器**对话框框中，指定**应用程序 ID**，**应用程序密钥**，和**租户 ID**为服务主体。 有关这些属性的详细信息，请参阅[这](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 单击 **“确定”** 关闭对话框。
4. 你可以看到你在“属性”  窗口中创建的连接管理器的属性。

