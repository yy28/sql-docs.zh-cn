---
description: Azure 资源管理器连接管理器
title: Azure 资源管理器连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 34accd71d7bd173b49ae9ee046e0eb5acdda220f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477959"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure 资源管理器连接管理器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


借助 Azure 资源管理器连接管理器****，SSIS 包能够使用[服务主体](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)管理 Azure 资源。

Azure 资源管理器连接管理器**** 是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组件。

若要创建和配置 Azure 资源管理器连接管理器****，请执行以下步骤：

1. 在“添加 SSIS 连接管理器” **** 对话框中，选择“AzureResourceManager”****，然后单击“添加”****。
2. 在“Azure 资源管理器连接管理器编辑器”**** 对话框中，为服务主体指定“应用程序 ID”****、“应用程序密钥”**** 和“租户 ID”****。 有关这些属性的详细信息，请参阅[这篇](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 单击“确定”  关闭对话框。
4. 你可以看到你在“属性” **** 窗口中创建的连接管理器的属性。
