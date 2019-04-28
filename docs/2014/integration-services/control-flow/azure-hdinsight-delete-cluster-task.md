---
title: Azure HDInsight 删除群集任务 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpdelcltask.f1
- sql11.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 839350610bdcc55d185fa06c122e71b50c5ca753
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832651"
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight 删除群集任务
Azure HDInsight 删除群集任务启用一个 SSIS 包来删除指定的 Azure 订阅和资源组中的一个 Azure HDInsight 群集。
  
> [!NOTE]
> 删除 HDInsight 群集可能需要 10~20 分钟。  
  
若要添加 **Azure HDInsight 删除群集任务**，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，  以查看以下 **Azure Blob 删除群集任务编辑器** 对话框。  
  
下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**说明**|  
|AzureResourceManagerConnection|选择一个现有 Azure 资源管理器连接管理器，或创建一个用于删除 HDInsight 群集的新连接管理器。|
|SubscriptionId|指定 HDInsight 群集所在的订阅的 ID。|
|ResourceGroup|指定 HDInsight 群集所在的 Azure 资源组。|
|ClusterName|指定要删除的群集的名称。|  
|FailIfNotExists|指定如果群集不存在时任务是否会失败。|
