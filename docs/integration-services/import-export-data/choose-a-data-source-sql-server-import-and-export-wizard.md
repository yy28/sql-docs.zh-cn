---
title: 选择数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 08baea2a92d21d9dca3a53dc17d6499f77e193d3
ms.sourcegitcommit: 5683044d87f16200888eda2c2c4dee38ff87793f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58222071"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>选择数据源（SQL Server 导入和导出向导）
  在欢迎页之后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“选择数据源”。 在此页上，需提供有关数据源以及如何连接到它的信息。
  
有关可以使用的数据源的信息，请参阅 [我可以使用哪些数据源和目标？](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导使用 SQL Server Integration Services (SSIS)。 因此，适用于 SSIS 的限制也同样适用于该向导。  例如，已按[数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)中所述默认添加了 ErrorCode 和 ErrorColumn 列。

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>“选择数据源”页面的屏幕截图 
下图显示了该向导“选择数据源”页的第一部分。 此页的其余部分含有数量不定的选项，具体取决于此处选择的数据源。

![选择源](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>选择数据源
 **数据源**  
通过选择可以连接到源的数据提供程序来指定数据源。

-   通常可轻松从名称判断出所需的数据提供程序，因为提供程序的名称通常包含数据源的名称（例如平面文件源、Microsoft Excel、Microsoft Access、用于 SqlServer 的 .Net Framework 数据提供程序以及用于 Oracle 的 .Net Framework 数据提供程序）。

-   如果有用于数据源的 ODBC 驱动程序，则选择用于 ODBC 的 .NET Framework 数据提供程序。 然后输入特定于驱动程序的信息。 ODBC 驱动程序不在数据源的下拉列表中列出。 用于 ODBC 的 .Net Framework 数据提供程序充当 ODBC 驱动程序的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **可用于数据源的访问接口可能不止一个。** 通常可以选择任何可用于源的提供程序。 例如，若要连接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以使用用于 SQL Server 的 .NET Framework 数据提供程序或 SQL Server ODBC 驱动程序。 （其他提供程序仍在列表中，但不再受支持。） 

## <a name="my-data-source-isnt-in-the-list"></a>我的数据源不在列表中
-   你可能需要从 Microsoft 或第三方下载数据提供程序。 “数据源”列表中可用数据提供程序的列表只包括计算机上安装的提供程序。 有关可以使用的数据源的信息，请参阅 [我可以使用哪些数据源和目标？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   你是否具备适用于你的数据源的 ODBC 驱动程序？ ODBC 驱动程序不在数据源的下拉列表中列出。 如果有用于数据源的 ODBC 驱动程序，则选择用于 ODBC 的 .NET Framework 数据提供程序。 然后输入特定于驱动程序的信息。 用于 ODBC 的 .Net Framework 数据提供程序充当 ODBC 驱动程序的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   64 位和 32 位提供程序 如果运行的是 64 位向导，则不会看到仅安装了 32 位提供程序的数据源，反之亦然。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

## <a name="after-you-choose-a-data-source"></a>选择数据源后
在选择数据源之后，“选择数据源”页面属性的其余部分具有数量不定的选项，具体取决于所选的数据提供程序。

要连接某个常用数据源，请参阅以下页面之一。
-   [连接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [连接到平面文件（文本文件）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 连接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Azure Blob 存储](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [连接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

有关如何连接到此处未列出的数据源的信息，请参阅[连接字符串参考](https://www.connectionstrings.com/)。 该第三方站点包含示例连接字符串、关于数据提供程序的详细信息以及它们需要的连接信息。

## <a name="whats-next"></a>下一步是什么？
 在提供有关数据源以及如何连接到它的信息后，下一个页面是“选择目标” 。 在此页上，需提供有关数据目标以及如何连接到它的信息。 有关详细信息，请参阅 [选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。

## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../../includes/paragraph-content/contribute-to-content.md)]