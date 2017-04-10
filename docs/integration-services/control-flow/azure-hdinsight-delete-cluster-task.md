---
title: "Azure HDInsight 删除群集任务 | Microsoft Docs"
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
  - "sql13.dts.designer.afpdelcltask.f1"
  - "sql14.dts.designer.afpdelcltask.f1"
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight 删除群集任务
  “Azure HDInsight 删除群集任务”启用一个 SSIS 包来删除指定 Azure 订阅中的一个 Azure HDInsight 群集。  
  
 “Azure HDInsight 删除群集任务”是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包组件。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
> [!NOTE]  
>  删除 HDInsight 群集通常需要花费 10 分钟。  
  
 若要添加“Azure HDInsight 删除群集任务”，可将其拖放到 SSIS 设计器，并双击或右键单击该任务，然后单击“编辑”，以查看下面的“Azure HDInsight 删除群集任务编辑器”对话框。  
  
 下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureSubscriptionConnection|选择一个现有的 Azure 订阅连接管理器或创建一个新的连接管理器，用于引用托管 HDInsight 群集的 Azure 订阅。|  
|ClusterName|指定要删除的群集的名称。|  
|FailIfNotExists|指定如果群集不存在时任务是否会失败。|  
  
  