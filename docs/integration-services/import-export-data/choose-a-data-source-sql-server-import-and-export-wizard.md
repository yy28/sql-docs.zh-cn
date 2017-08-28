---
title: "选择数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
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
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 80d35cb294fd900611c73ca37bba2a66baef0767
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>选择数据源（SQL Server 导入和导出向导）
  在欢迎页之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“选择数据源” 。 在此页上，需提供有关数据源以及如何连接到它的信息。
  
有关可以使用的数据源的信息，请参阅 [我可以使用哪些数据源和目标？](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>“选择数据源”页面的屏幕截图 
以下屏幕截图显示向导的“选择数据源”  页的第一部分。 网页的其余内容具有可变数量选项，这取决于你在此处选择的数据源。

![选择源](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>选择数据源
 **数据源**  
通过选择可以连接到源的数据提供程序来指定数据源。

-   **你需要的数据提供程序是从其名称通常明显**，因为提供程序的名称通常包含的名称的数据源中-例如，*平面文件*源、 Microsoft *Excel*，Microsoft*访问*，.Net Framework 数据提供程序*SqlServer*，.Net Framework 数据提供程序*Oracle*。

-   **如果你具有 ODBC 驱动程序的数据源**，选择.Net Framework Data Provider for ODBC。 然后输入特定于驱动程序的信息。 ODBC 驱动程序未列出在下拉列表中的数据源。 .Net Framework Data Provider for ODBC 充当 ODBC 驱动程序周围的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **可用于数据源的访问接口可能不止一个。** 通常可以选择任何可用于源的提供程序。 例如，若要连接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，你可以使用.NET Framework 数据提供程序为 SQL Server 或 SQL Server ODBC 驱动程序。 （其他提供程序也仍存在在列表中但不再受支持。） 

## <a name="my-data-source-isnt-in-the-list"></a>我的数据源不在列表中
-   **你可能需要下载的数据提供程序**来自 Microsoft 或第三方。 中的可用数据提供程序的列表**数据源**列表包含仅在计算机上安装的提供程序。 有关可以使用的数据源的信息，请参阅 [我可以使用哪些数据源和目标？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **你是否具有 ODBC 驱动程序为您的数据源？** ODBC 驱动程序未列出在下拉列表中的数据源。 如果你为数据源的 ODBC 驱动程序，选择.Net Framework Data Provider for ODBC。 然后输入特定于驱动程序的信息。 .Net Framework Data Provider for ODBC 充当 ODBC 驱动程序周围的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **64 位和 32 位提供程序。** 如果您在运行 64 位向导，你看不到数据源只能由 32 位提供商是安装，反之亦然。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。

## <a name="after-you-choose-a-data-source"></a>选择数据源后
选择数据源的其余部分后**选择数据源**页具有可变数量的选项，具体取决于你选择的数据提供程序。

若要连接到常用的数据源，请参阅以下页面之一。
-   [连接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [连接到平面文件 （文本文件）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 连接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Azure Blob 存储](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [连接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

有关如何连接到未在此处列出的数据源的信息，请参阅[该连接字符串引用](https://www.connectionstrings.com/)。 此第三方站点包含示例连接字符串以及有关数据提供程序的详细信息和它们需要的连接信息。

## <a name="whats-next"></a>下一步是什么？  
 在提供有关数据源以及如何连接到它的信息后，下一个页面是“选择目标” 。 在此页上，需提供有关数据目标以及如何连接到它的信息。 有关详细信息，请参阅 [选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。
 
## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



