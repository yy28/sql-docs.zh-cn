---
title: Azure 功能包 |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 771b7425ca166a05eb5290f576a7fa2cad3f19be
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52787039"
---
# <a name="azure-feature-pack"></a>Azure 功能包
用于 Azure 的 SQL Server Integration Services (SSIS) 功能包是一个扩展包，可为 SSIS 提供本页面上列出的组件，用于连接到 Azure 服务、在 Azure 与本地数据源之间传输数据以及处理 Azure 中存储的数据。

## <a name="components-in-the-feature-pack"></a>功能包中的组件
  
-   连接管理器  
  
    -   [Azure 存储连接管理器](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Azure 订阅连接管理器](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Azure Data Lake Store 连接管理器](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Azure 资源管理器连接管理器](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 连接管理器](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   “任务”  
  
    -   [Azure blob 上传任务](control-flow/azure-blob-upload-task.md)  
  
    -   [Azure Blob 下载任务](control-flow/azure-blob-download-task.md)  
  
    -   [Azure HDInsight Hive 任务](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Azure HDInsight Pig 任务](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Azure HDInsight 创建群集任务](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Azure HDInsight 删除群集任务](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 上传任务](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Azure Data Lake Store 文件系统任务](control-flow/file-system-task.md)    
  
-   数据流组件  
  
    -   [Azure Blob 源](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Azure Blob 目标](data-flow/azure-blob-destination.md)  
    
    -   [Azure Data Lake Store 源](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 目标](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Azure Blob 枚举器和 ADLS 文件枚举器。 请参阅 [Foreach Loop Container](control-flow/foreach-loop-container.md)。  
  
 
## <a name="download-the-feature-pack"></a>下载功能包  
下载用于 Azure 的 SQL Server Integration Services (SSIS) 功能包。  
  
-   [Microsoft SQL Server 2014 Integration Services 功能用于 Azure 的包](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>先决条件  
必须在安装此功能包之前安装以下系统必备组件。  
  
-   SQL Server Integration Services  
-   .Net Framework 4.5  
  
## <a name="scenarios"></a>方案  
  
### <a name="big-data-processing"></a>大数据处理  
 使用 Azure Connector 可完成以下大数据处理工作：  
  
1.  使用 Azure Blob 上载任务可将输入数据上载到 Azure Blob 存储。  
  
2.  使用 Azure HDInsight 创建群集任务可创建 Azure HDInsight 群集。 如果要使用自己的群集，则此步骤是可选的。  
  
3.  使用 Azure HDInsight Hive 任务或 Azure HDInsight Pig 任务可在 Azure HDInsight 群集上调用 Pig 或 Hive 作业。  
  
4.  使用 Azure HDInsight 删除群集任务可在使用之后删除 HDInsight 群集（如果在步骤 #2 中创建了按需 HDInsight 群集）。  
  
5.  使用 Azure HDInsight Blob 下载任务可从 Azure Blob 存储下载 Pig/Hive 输出数据。  
  
 ![SSIS AzureConnector BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "SSIS AzureConnector BigDataScenario")  
  
### <a name="cloud-data-archiving"></a>云数据存档  
 使用 SSIS 包中的 Azure Blob 目标可将输出数据写入 Azure Blob 存储，或使用 Azure Blob 源可从 Azure Blob 存储读取数据。  
  
 ![SSIS AzureConnector CloudArchive 1](media/ssis-azureconnector-cloudarchive-1.png "SSIS AzureConnector CloudArchive 1")  
  
 ![SSIS AzureConnector CloudArchive 2](media/ssis-azureconnector-cloudarchive-2.png "SSIS AzureConnector CloudArchive 2")  
  
 将 Foreach 循环容器与 Azure Blob 枚举器一起使用可处理多个 bob 文件中的数据。  
  
 ![SSIS AzureConnector CloudArchive 3](media/ssis-azureconnector-cloudarchive-3.png "SSIS AzureConnector CloudArchive 3")  
  
  
