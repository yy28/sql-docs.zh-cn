---
title: Azure 存储连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
manager: craigg
ms.openlocfilehash: a46945b7c7725d680fb303a451327dc2733642aa
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277826"
---
# <a name="azure-storage-connection-manager"></a>Azure 存储连接管理器
  通过使用你为以下属性指定的值，Azure 存储连接管理器使 SSIS 包能够连接到 Azure 存储帐户：存储帐户名称和帐户密钥。  
   
 Azure 存储连接管理器是[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的一个组件。 
  
1.  在“添加 SSIS 连接管理器”  对话框中，选择“AzureStorage” ，然后单击“添加” 。  
  
2.  在“Azure 存储连接管理器编辑器”对话框中，选择“使用 Azure 帐户”  以通过 Internet 连接到 Azure 存储服务，或选择“使用本地开发人员帐户”  以连接到 Azure 存储模拟器承载的本地服务。  
  
3.  如果选择了“使用 Azure 帐户”  选项，请执行以下操作：  
  
    1.  为“存储帐户名称”  和“帐户密钥”  字段指定值。 这些值将存储为 SSIS 包中的敏感数据。  
  
    2.  如果你想要使用 HTTPS 而不是 HTTP 来连接到 Azure 存储服务，请选择“使用 HTTPS”  。  
  
4.  单击 **“确定”** 关闭对话框。  
  
5.  你可以看到你在“属性”  窗口中创建的连接管理器的属性。  
  
  
