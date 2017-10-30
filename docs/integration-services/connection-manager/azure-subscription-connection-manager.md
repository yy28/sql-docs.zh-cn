---
title: "Azure 订阅连接管理器 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f34ac8d5c1b6bd117a83d287db1d46ff6f786aab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-subscription-connection-manager"></a>Azure 订阅连接管理器
  通过使用你为以下属性指定的值， **Azure 订阅连接管理器** 使 SSIS 包能够连接到 Azure 订阅：Azure 订阅 ID 和管理证书。  
  
 **Azure 订阅连接管理器**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
1.  在如上所示的“添加 SSIS 连接管理器”  对话框中，选择“Azure 订阅” ，然后单击“添加” 。  你应该会看到  “Azure 订阅连接管理器编辑器”对话框。  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  为“Azure 订阅 ID” 输入你的 Azure 订阅 ID，它可以唯一标识 Azure 订阅。  可以在 **设置** 页下的 [Azure 管理门户](https://manage.windowsazure.com) 上找到这些值：  
  
    ![SSIS AzureSettings SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS AzureSettings SubscriptionID")  
  
3.  从下拉列表中选择“管理证书存储位置”和“管理证书存储名称”。  
  
4.  输入**管理证书指纹**或单击“浏览...” “浏览…”，从所选存储中选择一个证书。 必须将证书作为订阅的管理证书上载。 为此，请在以下 Azure 门户页上单击“上传”（请参阅这篇 [MSDN 帖子](https://msdn.microsoft.com/library/azure/gg551722.aspx)以了解详细信息）。  
  
     ![管理证书 AzureSettings SSIS](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "管理证书 AzureSettings SSIS")  
  
5.  单击“测试连接”  以测试连接。  
  
6.  单击 **“确定”** 关闭对话框。  
  
  

