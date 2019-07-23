---
title: 用于 Integration Services (SSIS) 的Azure 功能包 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a5513c6f1f326984c93a760afdd88f949dc18b02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68007986"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>用于 Azure 的 Integration Services (SSIS) 功能包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


用于 Azure 的 SQL Server Integration Services (SSIS) 功能包是一个扩展包，可为 SSIS 提供本页面上列出的组件，用于连接到 Azure 服务、在 Azure 与本地数据源之间传输数据以及处理 Azure 中存储的数据。

[![下载用于 Azure 的 SSIS 功能包](../analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=54798)下载 

- 对于 SQL Server 2017 - [用于 Azure 的 Microsoft SQL Server 2017 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=54798)
- 对于 SQL Server 2016 - [用于 Azure 的 Microsoft SQL Server 2016 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=49492)
- 对于 SQL Server 2014 - [用于 Azure 的 Microsoft SQL Server 2014 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=47366)
- 对于 SQL Server 2012 - [用于 Azure 的 Microsoft SQL Server 2012 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=47367)

下载页面还包含有关先决条件的信息。 在将 Azure 功能包安装到服务器上之前，确保已安装 SQL Server，否则在将功能包部署到服务器上的 SSIS 目录数据库 SSISDB 时，功能包中的组件可能不可用。

## <a name="components-in-the-feature-pack"></a>功能包中的组件
-   连接管理器

    -   [Azure Data Lake Analytics Connection Manager](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Azure Data Lake Store 连接管理器](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure HDInsight 连接管理器](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Azure 资源管理器连接管理器](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure 存储连接管理器](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 订阅连接管理器](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   “任务”

    -   [Azure Blob 下载任务](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure blob 上传任务](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Data Lake Analytics 任务](control-flow/azure-data-lake-analytics-task.md)

    -   [Azure Data Lake Store 文件系统任务](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Azure HDInsight 创建群集任务](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 删除群集任务](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure HDInsight Hive 任务](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 任务](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure SQL DW 上传任务](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [灵活的文件任务](../integration-services/control-flow/flexible-file-task.md)

-   数据流组件

    -   [Azure Blob 源](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 目标](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 源](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 目标](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [灵活的文件源](../integration-services/data-flow/flexible-file-source.md)

    -   [灵活的文件目标](../integration-services/data-flow/flexible-file-destination.md)

-   Azure Blob、Azure Data Lake Store 和 Data Lake Storage Gen2 文件枚举器。 请参阅 [Foreach 循环容器](../integration-services/control-flow/foreach-loop-container.md)

## <a name="scenario-processing-big-data"></a>方案：处理大数据
 使用 Azure Connector 可完成以下大数据处理工作：

1.  使用 Azure Blob 上载任务可将输入数据上载到 Azure Blob 存储。

2.  使用 Azure HDInsight 创建群集任务可创建 Azure HDInsight 群集。 如果要使用自己的群集，则此步骤是可选的。

3.  使用 Azure HDInsight Hive 任务或 Azure HDInsight Pig 任务可在 Azure HDInsight 群集上调用 Pig 或 Hive 作业。

4.  使用 Azure HDInsight 删除群集任务可在使用之后删除 HDInsight 群集（如果在步骤 #2 中创建了按需 HDInsight 群集）。

5.  使用 Azure HDInsight Blob 下载任务可从 Azure Blob 存储下载 Pig/Hive 输出数据。

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>方案：管理云中的数据
 在 SSIS 包中使用 Azure blob 目标，将输出数据写入 Azure blob 存储区；或使用 Azure blob 源，从 Azure blob 存储区中读取数据。

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 结合使用 Foreach 循环容器和 Azure blob 枚举器，处理多个 blob 文件中的数据。

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  
