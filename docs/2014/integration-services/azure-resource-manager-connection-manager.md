---
title: Azure 资源管理器连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2db468ae6a9bc90c492a9c4557d248f7f7ef81d1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84925224"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure 资源管理器连接管理器
借助 Azure 资源管理器连接管理器  ，SSIS 包能够使用[服务主体](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)管理 Azure 资源。

若要创建和配置 Azure 资源管理器连接管理器****，请执行以下步骤：

1. 在“添加 SSIS 连接管理器” **** 对话框中，选择“AzureResourceManager”****，然后单击“添加”****。
2. 在“Azure 资源管理器连接管理器编辑器”**** 对话框中，为服务主体指定“应用程序 ID”****、“应用程序密钥”**** 和“租户 ID”****。 有关这些属性的详细信息，请参阅[这篇](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 单击“确定”  关闭对话框。
4. 你可以看到你在“属性” **** 窗口中创建的连接管理器的属性。
