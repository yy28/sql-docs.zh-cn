---
title: "Azure HDInsight Pig 任务 | Microsoft Docs"
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
  - "sql13.dts.designer.afppigtask.f1"
  - "sql14.dts.designer.afppigtask.f1"
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight Pig 任务
  使用 **“Azure HDInsight Pig 任务”** 在 Azure HDInsight 群集上运行 Pig 脚本。 
    
若要添加“Azure HDInsight Pig 任务”，可将其拖放到 SSIS 设计器，并双击或右键单击该任务，然后单击“编辑”，以查看以下“Azure HDInsight Pig 任务编辑器”对话框。  
  
 “Azure HDInsight Pig 任务”是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包组件。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
1.  对于 **AzureSubscriptionConnection** 字段，请选择现有的 Azure 订阅连接管理器或创建一个新的连接管理器，用于引用托管 HDInsight 群集的 Azure 订阅。  
  
2.  对于 **HDInsightClusterName** 字段，请输入要在其上运行 Pig 脚本的 HDInsight 群集的名称。  
  
3.  对于 **LocalLogFolder** 字段，请单击“...”（省略号），然后选择要将 Pig 处理日志从 HDInsight 群集中下载到其中的文件夹。  
  
4.  可以通过以下两种方法指定 Pig 脚本：  
  
    1.  **内联脚本**：单击“脚本”字段旁的“...”（省略号），然后在“输入脚本”对话框中键入内联脚本。  
  
    2.  “脚本文件”：将脚本文件上传到 blob 位置并指定其“” 。 如果该 blob 不在 HDInsight 群集的默认存储空间或容器中，则必须指定“ExternalStorageAccountName”  和“ExternalBlobContainer”  。 对于外部 blob，请确保它已配置为可公开访问。  
  
     如果同时指定两者，则将使用脚本文件并忽略内联脚本。  
  
  