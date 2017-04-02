---
title: "Azure HDInsight 创建群集任务 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpcreatecltask.f1"
  - "sql14.dts.designer.afpcreatecltask.f1"
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Azure HDInsight 创建群集任务
  “Azure HDInsight 创建群集任务”启用一个 SSIS 包来创建指定的 Azure 订阅中的一个 Azure HDInsight 群集。  
  
 “Azure HDInsight 创建群集任务”是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包组件。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
> [!NOTE]  
>  -   创建新的 HDInsight 群集通常需要花费 10 分钟。  
> -   没有与创建和运行 Azure HDInsight 群集相关的成本。 有关详细信息，请参阅 [HDInsight 定价](http://azure.microsoft.com/en-us/pricing/details/hdinsight/)主题。  
  
 若要添加“Azure HDInsight 创建群集任务”，可将其拖放到 SSIS 设计器，然后双击或右键单击，再单击“编辑”以查看以下“Azure HDInsight 创建群集任务编辑器”对话框。  
  
 下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureSubscriptionConnection|选择一个现有的 Azure 订阅连接管理器或创建一个新的连接管理器，用于引用托管 HDInsight 群集的 Azure 订阅。|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器；或者创建一个新的连接管理器，该管理器引用将与 HDInsight 群集关联的 Azure 存储帐户。|  
|位置|指定 HDInsight 群集的位置。 必须在与 Azure 存储相同的位置中创建群集。|  
|ClusterName|指定要创建的 HDInsight 群集的名称。|  
|ClusterSize|指定希望群集中包含的节点数。|  
|BlobContainer|指定与 HDInsight 群集相关联的默认存储容器的名称。|  
|UserName|指定具有群集访问权限的用户的名字。|  
|密码|指定用户的密码。|  
|FailIfExists|指定如果群集已存在时任务是否失败。|  
  
> [!NOTE]  
>  HDInsight 群集和 Azure 存储的位置必须相同。  
  
  