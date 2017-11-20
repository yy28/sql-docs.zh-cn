---
title: "Azure HDInsight 创建群集任务 |Microsoft 文档"
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
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 71a24dc15253916c32b07e6024e2ab32514c9d39
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight 创建群集任务
**Azure HDInsight 创建群集任务**允许 SSIS 包以在指定的 Azure 订阅和资源组中创建 Azure HDInsight 群集。
  
**Azure HDInsight 创建群集任务**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
> [!NOTE]  
> - 创建新的 HDInsight 群集可能需要花费 10 ~ 20 分钟。  
> - 没有与创建和运行 Azure HDInsight 群集关联的成本。 请参阅[HDInsight 定价](http://azure.microsoft.com/en-us/pricing/details/hdinsight/)有关详细信息。  
  
若要添加“Azure HDInsight 创建群集任务”，可将其拖放到 SSIS 设计器，然后双击或右键单击，再单击“编辑”以查看以下“Azure HDInsight 创建群集任务编辑器”对话框。  
  
下表提供了在此对话框中的字段的说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureResourceManagerConnection|选择现有 Azure 资源管理器连接管理器或创建一个将用于创建 HDInsight 群集的新。|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器；或者创建一个新的连接管理器，该管理器引用将与 HDInsight 群集关联的 Azure 存储帐户。|
|subscriptionId|指定将在其中创建 HDInsight 群集的订阅的 ID。|
|资源组|指定 Azure 资源组中，将在创建群集的 HDInsight。|
|位置|指定 HDInsight 群集的位置。 必须在与指定的 Azure 存储帐户相同的位置中创建群集。|  
|ClusterName|指定要创建的 HDInsight 群集的名称。|  
|ClusterSize|指定要在群集创建节点的数。|  
|BlobContainer|指定要与 HDInsight 群集相关联的默认存储容器的名称。|  
|UserName|指定要用于连接到 HDInsight 群集的用户名。|  
|密码|指定要用于连接到 HDInsight 群集的密码。|
|SshUserName|指定用于远程访问 HDInsight 群集使用 SSH 的用户名称。|
|SshPassword|指定用于远程访问 HDInsight 群集使用 SSH 的密码。|
|FailIfExists|指定如果群集已存在时任务是否失败。|  
  
> [!NOTE]  
> HDInsight 群集和 Azure 存储帐户的位置必须相同。

