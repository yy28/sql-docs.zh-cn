---
title: "Azure HDInsight 删除群集任务 |Microsoft 文档"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f98b69e8bd3b2e78f6dd20a19ca17a83a834c3b3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight 删除群集任务
**Azure HDInsight 删除群集任务**允许 SSIS 包将删除指定的 Azure 订阅和资源组中的 Azure HDInsight 群集。
  
**Azure HDInsight 删除群集任务**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
> [!NOTE]
> 删除 HDInsight 群集可能需要 10 ~ 20 分钟。  
  
若要添加 **Azure HDInsight 删除群集任务**，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，  以查看以下 **Azure Blob 删除群集任务编辑器** 对话框。  
  
下表提供了在对话框中的字段的说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureResourceManagerConnection|选择现有 Azure 资源管理器连接管理器或创建一个将用于删除 HDInsight 群集的新。|
|subscriptionId|指定 HDInsight 群集的订阅的 ID。|
|资源组|指定 HDInsight 群集中的 Azure 资源组。|
|ClusterName|指定要删除的群集的名称。|  
|FailIfNotExists|指定如果群集不存在时任务是否会失败。|

