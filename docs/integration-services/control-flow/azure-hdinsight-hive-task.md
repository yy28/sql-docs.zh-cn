---
title: "Azure HDInsight Hive 任务 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f9e67e91b5cd38482ab1151d5942c9c55c04136c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-hive-task"></a>Azure HDInsight Hive 任务
使用“Azure HDInsight Hive 任务”  在 Azure HDInsight 群集上运行 Hive 脚本。
     
若要添加“Azure HDInsight Hive 任务”，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，以查看以下“Azure HDInsight Hive 任务编辑器”对话框。  
  
**Azure HDInsight Hive 任务**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
 以下列表介绍了此对话框中的字段。  
  
1.  有关**HDInsightConnection**字段中，选择一个现有的 Azure HDInsight 连接管理器或创建一个新的一个 Azure HDInsight 群集是指用于执行脚本。
  
2.  有关**AzureStorageConnection**字段中，选择一个现有的 Azure 存储连接管理器或创建一个新的一个引用 Azure 存储帐户与群集关联。 此操作才有必要，如果你想要下载的脚本执行的输出和错误日志。
 
3.  有关**BlobContainer**字段中，指定与群集关联的存储容器名称。 此操作才有必要，如果你想要下载的脚本执行的输出和错误日志。
  
4.  有关**LocalLogFolder**字段中，指定到下载的脚本执行的输出和错误日志的文件夹。 此操作才有必要，如果你想要下载的脚本执行的输出和错误日志。   
  
5.  有两种方法来指定要执行的 Hive 脚本：
  
    1.  **行脚本**： 指定**脚本**通过键入的字段中，线脚本要在中执行**输入脚本**对话框。
  
    2.  **脚本文件**： 将脚本文件上载到 Azure Blob 存储并指定**BlobName**字段。 如果 blob 不在默认存储帐户或容器与 HDInsight 群集关联**ExternalStorageAccountName**和**ExternalBlobContainer**必须指定字段。 对于外部 blob，请确保它已配置为公开访问。  
  
     如果同时指定了，将使用脚本文件，并以串联脚本将被忽略。

