---
title: "Azure HDInsight Hive 任务 | Microsoft Docs"
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
  - "sql13.dts.designer.afphivetask.f1"
  - "sql14.dts.designer.afphivetask.f1"
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure HDInsight Hive 任务
  使用“Azure HDInsight Hive 任务”  在 Azure HDInsight 群集上运行 Hive 脚本。
     
若要添加“Azure HDInsight Hive 任务”，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，以查看以下“Azure HDInsight Hive 任务编辑器”对话框。  
  
 “Azure HDInsight Hive 任务”是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包组件。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
 以下列表介绍了此对话框中的字段。  
  
1.  在“AzureSubscriptionConnection”  字段中，选择现有的 Azure 订阅连接管理器，或创建一个新的 Azure 连接管理器用于引用承载 HDInsight 群集的 Azure 订阅。  
  
2.  在“HDInsightClusterName”  字段中，选择要在其上运行 Hive 脚本的 HDInsight 群集的名称。  
  
3.  在“LocalLogFolder”字段中，单击“...”（省略号），然后选择要将 Hive 处理日志从 HDInsight 群集中下载到其中的文件夹。  
  
4.  有两种方法可指定 Hive 脚本：  
  
    1.  **内联脚本**：单击“脚本”字段旁的“...”（省略号），然后在“输入脚本”对话框中键入内联脚本。  
  
    2.  “脚本文件”：将脚本文件上传到 blob 位置并指定其“” 。 如果该 blob 不在 HDInsight 群集的默认存储空间或容器中，则必须指定“ExternalStorageAccountName”  和“ExternalBlobContainer”  。 对于外部 blob，请确保它已配置为可公开访问。  
  
     如果同时指定两者，则将使用脚本文件并忽略内联脚本。  
  
  