---
title: "连接到 Azure Blob 存储 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 36b992b5141799d4e168b2e990643e6a515a8d69
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>连接到 Azure Blob 存储 （SQL Server 导入和导出向导）
本主题演示如何连接到**Azure Blob 存储**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。

>   [!NOTE]
> 若要使用的 Azure Blob 源或目标，必须安装用于 SQL Server Integration Services 的 Azure 功能包。
> - 若要下载功能包，请参阅[Microsoft SQL Server 2016 Integration Services 功能包 azure](https://www.microsoft.com/download/details.aspx?id=49492)。
>
> - 有关详细信息，请参阅[用于 Integration Services 的 Azure 功能包 (SSIS)](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

下面的屏幕快照显示的选项配置与 Azure Blob 存储的连接。

![Azure Blob 存储 连接](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>若要指定的选项

> [!NOTE]
> Azure Blob 存储是否您的源或目标，此数据提供程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

 **使用 Azure 帐户**  
 指定是否使用联机帐户。
  
 **存储帐户名称**  
 输入 Azure 存储帐户的名称。  
  
**帐户密钥**  
输入 Azure 存储帐户的密钥。  
  
 **使用 HTTPS**  
 指定是使用 HTTP 还是 HTTPS 连接到存储帐户。  
  
 **使用本地开发人员帐户**  
 指定是否在本地计算机上使用存储仿真程序。  
  
 **Blob 容器名称**  
 从指定的存储帐户中可用的存储容器列表中选择。  
  
 **Blob 文件格式**  
 选择文本或 Avro 文件格式。  
  
 **列分隔符字符**  
 如果您选择文本格式，输入列分隔符字符。  
  
 **使用第一行作为列名称**  
 指定第一行数据是否包含列名称。  

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


