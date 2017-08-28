---
title: "选择目标 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 4ff3c7c8413bd6b535e1c5f95e2a7b06b397c053
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>选择目标（SQL Server 导入和导出向导）
 在提供有关数据源以及如何连接到它的信息后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“选择目标” 。 在此页上，需提供有关数据目标以及如何连接到它的信息。
  
若要了解可使用的数据目标，请参阅 [可使用哪些数据源和目标？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)。 

## <a name="screen-shot-of-the-destination-page"></a>“目标”页面的屏幕截图
以下屏幕截图显示的是该向导的“选择目标”  页的第一部分。 网页的其余内容具有可变数量选项，这取决于你在此处选择的目标。

![选择目标](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>选择目标
 **目标**  
 通过选择可以将数据导入到目标中的数据提供程序来指定目标。
 
-   **你需要的数据提供程序是从其名称通常明显**，因为提供程序的名称通常包含目标的名称，如*平面文件*目的，Microsoft *Excel*，Microsoft*访问*，.Net Framework 数据提供程序*SqlServer*，.Net Framework 数据提供程序*Oracle*。

-   **如果必须为你的目标的 ODBC 驱动程序**，选择.Net Framework Data Provider for ODBC。 然后输入特定于驱动程序的信息。 ODBC 驱动程序不在目标中的下拉列表中列出。 .Net Framework Data Provider for ODBC 充当 ODBC 驱动程序周围的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **可用于目标的访问接口可能不止一个。** 通常可以选择任何可用于目标的访问接口。 例如，若要连接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，你可以使用.NET Framework 数据提供程序为 SQL Server 或 SQL Server ODBC 驱动程序。 （其他提供程序也仍存在在列表中但不再受支持。） 

## <a name="my-destination-isnt-in-the-list"></a>我目标不在列表中
-   **你可能需要下载的数据提供程序**来自 Microsoft 或第三方。 中的可用数据提供程序的列表**目标**列表包含仅在计算机上安装的提供程序。 你可以使用的目标有关的信息，请参阅[使用哪种数据源和目标可以我？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **你是否具有 ODBC 驱动程序为目标？** ODBC 驱动程序不在目标中的下拉列表中列出。 如果你为你的目标的 ODBC 驱动程序，选择.Net Framework Data Provider for ODBC。 然后输入特定于驱动程序的信息。 .Net Framework Data Provider for ODBC 充当 ODBC 驱动程序周围的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **64 位和 32 位提供程序。** 如果您在运行 64 位向导，你看不到目标的 32 位提供程序是安装，反之亦然。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。

## <a name="after-you-choose-a-destination"></a>选择目标之后
选择目标的其余部分后**选择目标**页具有可变数量的选项，具体取决于你选择的数据提供程序。

若要连接到常用的目标，请参阅以下页面之一。
-   [连接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [连接到平面文件 （文本文件）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 连接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Azure Blob 存储](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [连接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

有关如何连接到的目标，未在此处列出的信息，请参阅[该连接字符串引用](https://www.connectionstrings.com/)。 此第三方站点包含示例连接字符串以及有关数据提供程序的详细信息和它们需要的连接信息。

## <a name="whats-next"></a>下一步是什么？  
 提供有关数据目标以及有关如何连接到它的信息之后，下一页是“指定表复制或查询” 。 在此页上，可指定要复制整个表还是仅复制特定行。 有关详细信息，请参阅 [指定表复制或查询](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



