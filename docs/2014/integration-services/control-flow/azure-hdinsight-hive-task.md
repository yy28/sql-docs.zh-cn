---
title: Azure HDInsight Hive 任务 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afphivetask.f1
- sql11.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5905dee4a7a195a16d217b28b59cc10bb74dd9a9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433874"
---
# <a name="azure-hdinsight-hive-task"></a>Azure HDInsight Hive 任务
使用“Azure HDInsight Hive 任务”  在 Azure HDInsight 群集上运行 Hive 脚本。
     
若要添加“Azure HDInsight Hive 任务”  ，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”  ，以查看以下“Azure HDInsight Hive 任务编辑器”  对话框。  
  
 以下列表介绍了此对话框中的字段。  
  
1.  对于 HDInsightConnection 字段，请选择一个现有 Azure HDInsight 连接管理器，或创建一个新的连接管理器，引用用于执行脚本的 Azure HDInsight 群集****。
  
2.  对于 AzureStorageConnection 字段，请选择一个现有 Azure 存储连接管理器，或创建一个新的连接管理器，引用与群集关联的 Azure 存储帐户****。 只有在需要下载脚本执行输出和错误日志时，才需要执行此操作。
 
3.  对于 BlobContainer 字段，指定与群集关联的存储容器名称****。 只有在需要下载脚本执行输出和错误日志时，才需要执行此操作。
  
4.  对于 LocalLogFolder 字段，指定脚本执行输出和错误日志要下载到的文件夹****。 只有在需要下载脚本执行输出和错误日志时，才需要执行此操作。   
  
5.  可通过两种方法指定要执行的 Hive 脚本：
  
    1.  **内联脚本**：通过在“输入脚本”对话框中键入要执行的内联脚本来指定“脚本”字段********。
  
    2.  **脚本文件**：将脚本文件上传到 Azure Blob 存储，并指定 BlobName 字段****。 如果该 blob 不在默认存储帐户或与 HDInsight 群集关联的容器中，则必须指定 ExternalStorageAccountName 和 ExternalBlobContainer 字段********。 对于外部 blob，请确保它已配置为可公开访问。  
  
     如果同时指定两者，则使用脚本文件并忽略内联脚本。
