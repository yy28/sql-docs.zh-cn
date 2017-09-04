---
title: "Azure Feature Pack for Integration Services (SSIS) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4941d8eb846e9d47b008447fe0e346d43de5d87f
ms.openlocfilehash: d4204ba56e515025bed3ae3bf8e7a77d6da471be
ms.contentlocale: zh-cn
ms.lasthandoff: 08/30/2017

---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>用于 Azure 的 Integration Services (SSIS) 功能包
SQL Server Integration Services (SSIS) 功能适用于 Azure 的包是在 SSIS 以连接到 Azure 服务，Azure 和本地数据源和处理存储在 Azure 中的数据之间的传输数据的此页提供列出的组件的扩展。

[![下载 SSIS Feature Pack for Azure](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=54798) **下载**

- SQL server 自 2017 年 1- [Microsoft SQL Server 自 2017 年 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- SQL server 2016- [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- SQL server 2014- [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47366)
- 针对 SQL Server 2012 的[Microsoft SQL Server 2012 Integration Services Feature Pack for Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47367)

## <a name="components-in-the-feature-pack"></a>功能包中的组件
-   连接管理器

    -   [Azure 存储连接管理器](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 订阅连接管理器](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Azure Data Lake Store 连接管理器](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure 资源管理器连接管理器](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 连接管理器](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

-   “任务”

    -   [Azure blob 上传任务](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Blob 下载任务](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure HDInsight Hive 任务](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 任务](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure HDInsight 创建群集任务](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 删除群集任务](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 上传任务](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Azure 数据湖存储文件系统任务](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

-   数据流组件

    -   [Azure Blob 源](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 目标](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 源](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 目标](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   Azure Blob （&) ADLS 文件枚举器。 请参阅[Foreach 循环容器](http://msdn.microsoft.com/library/95a19dde-61ca-4d9b-aa3d-131fa4264296)

## <a name="download-the-feature-pack"></a>下载功能包
 下载用于 Azure 的 SQL Server Integration Services (SSIS) 功能包。
 
- [SSIS 用于 Azure 功能包](http://go.microsoft.com/fwlink/?LinkID=626967)for SQL Server 2016
- [SSIS 用于 Azure 功能包](https://www.microsoft.com/en-us/download/details.aspx?id=54798)为[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

## <a name="prerequisites"></a>必要條件
 必须在安装此功能包之前安装以下系统必备组件。

-   SQL Server Integration Services
-   .Net Framework 4.5

## <a name="scenario-processing-big-data"></a>应用场景：处理大数据
 使用 Azure Connector 可完成以下大数据处理工作：

1.  使用 Azure Blob 上载任务可将输入数据上载到 Azure Blob 存储。

2.  使用 Azure HDInsight 创建群集任务可创建 Azure HDInsight 群集。 如果要使用自己的群集，则此步骤是可选的。

3.  使用 Azure HDInsight Hive 任务或 Azure HDInsight Pig 任务可在 Azure HDInsight 群集上调用 Pig 或 Hive 作业。

4.  使用 Azure HDInsight 删除群集任务可在使用之后删除 HDInsight 群集（如果在步骤 #2 中创建了按需 HDInsight 群集）。

5.  使用 Azure HDInsight Blob 下载任务可从 Azure Blob 存储下载 Pig/Hive 输出数据。

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>应用场景：管理云数据
 在 SSIS 包中使用 Azure blob 目标，将输出数据写入 Azure blob 存储区；或使用 Azure blob 源，从 Azure blob 存储区中读取数据。

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 结合使用 Foreach 循环容器和 Azure blob 枚举器，处理多个 blob 文件中的数据。

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  

