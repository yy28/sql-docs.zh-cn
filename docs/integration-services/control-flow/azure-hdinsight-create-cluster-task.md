---
title: Azure HDInsight 创建群集任务 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3027e92db0b0dd4270f28c8efc01a32f5558562d
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402099"
---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight 创建群集任务
“Azure HDInsight 创建群集任务”启用一个 SSIS 包来创建指定的 Azure 订阅和资源组中的一个 Azure HDInsight 群集。
  
“Azure HDInsight 创建群集任务”是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组件。
  
> [!NOTE]  
> - 新建 HDInsight 群集可能需要花费 10~20 分钟。  
> - 这里存在与创建和运行 Azure HDInsight 群集相关的成本。 有关详细信息，请参阅 [HDInsight 定价](http://azure.microsoft.com/pricing/details/hdinsight/)。  
  
若要添加“Azure HDInsight 创建群集任务”，可将其拖放到 SSIS 设计器，然后双击或右键单击，再单击“编辑”以查看以下“Azure HDInsight 创建群集任务编辑器”对话框。  
  
下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureResourceManagerConnection|选择一个现有的 Azure 资源管理器连接管理器，或创建一个用于创建 HDInsight 群集的新连接管理器。|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器；或者创建一个新的连接管理器，该管理器引用将与 HDInsight 群集关联的 Azure 存储帐户。|
|SubscriptionId|指定将在其中创建 HDInsight 群集的订阅的 ID。|
|ResourceGroup|指定将在其中创建 HDInsight 群集的 Azure 资源组。|
|位置|指定 HDInsight 群集的位置。 必须在与指定的 Azure 存储账户相同的位置创建群集。|  
|ClusterName|指定要创建的 HDInsight 群集的名称。|  
|ClusterSize|指定要在群集中创建的节点数。|  
|BlobContainer|指定要与 HDInsight 群集相关联的默认存储容器的名称。|  
|UserName|指定用于连接到 HDInsight 群集的用户名。|  
|Password|指定用于连接到 HDInsight 群集的密码。|
|SshUserName|指定使用 SSH 远程访问 HDInsight 群集时使用的用户名称。|
|SshPassword|指定使用 SSH 远程访问 HDInsight 群集的密码。|
|FailIfExists|指定如果群集已存在时任务是否失败。|  
  
> [!NOTE]  
> HDInsight 群集和 Azure 存储帐户的位置必须相同。
