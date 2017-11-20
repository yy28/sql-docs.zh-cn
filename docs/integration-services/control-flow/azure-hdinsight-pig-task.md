---
title: "Azure HDInsight Pig 任务 |Microsoft 文档"
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
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9874b119b634966b146f8fa9d22c016bcd91617b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-pig-task"></a>Azure HDInsight Pig 任务
使用 **“Azure HDInsight Pig 任务”** 在 Azure HDInsight 群集上运行 Pig 脚本。
     
若要添加“Azure HDInsight Pig 任务”，可将其拖放到 SSIS 设计器，并双击或右键单击该任务，然后单击“编辑”，以查看以下“Azure HDInsight Pig 任务编辑器”对话框。  
  
**Azure HDInsight Pig 任务**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
 以下列表介绍了此对话框中的字段。  
  
1.  有关**HDInsightConnection**字段中，选择一个现有的 Azure HDInsight 连接管理器或创建一个新的一个 Azure HDInsight 群集是指用于执行脚本。
  
2.  有关**AzureStorageConnection**字段中，选择一个现有的 Azure 存储连接管理器或创建一个新的一个引用 Azure 存储帐户与群集关联。 此操作才有必要，如果你想要下载的脚本执行的输出和错误日志。
 
3.  有关**BlobContainer**字段中，指定与群集关联的存储容器名称。 此操作才有必要，如果你想要下载的脚本执行的输出和错误日志。
  
4.  有关**LocalLogFolder**字段中，指定到下载的脚本执行的输出和错误日志的文件夹。 此操作才有必要，如果你想要下载的脚本执行的输出和错误日志。   
  
5.  有两种方法来指定要执行的 Pig 脚本：
  
    1.  **行脚本**： 指定**脚本**通过键入的字段中，线脚本要在中执行**输入脚本**对话框。
  
    2.  **脚本文件**： 将脚本文件上载到 Azure Blob 存储并指定**BlobName**字段。 如果 blob 不在默认存储帐户或容器与 HDInsight 群集关联**ExternalStorageAccountName**和**ExternalBlobContainer**必须指定字段。 对于外部 blob，请确保它已配置为公开访问。  
  
     如果同时指定了，将使用脚本文件，并以串联脚本将被忽略。

