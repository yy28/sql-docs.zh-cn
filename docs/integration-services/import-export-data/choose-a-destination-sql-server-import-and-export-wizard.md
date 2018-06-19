---
title: 选择目标（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e08d09bacbd4bdc6a03c89d258c2744a76296038
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404519"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>选择目标（SQL Server 导入和导出向导）
 在提供有关数据源以及如何连接到它的信息后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“选择目标” 。 在此页上，需提供有关数据目标以及如何连接到它的信息。
  
若要了解可使用的数据目标，请参阅 [可使用哪些数据源和目标？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)。 

## <a name="screen-shot-of-the-destination-page"></a>“目标”页面的屏幕截图
以下屏幕截图显示的是该向导的“选择目标”  页的第一部分。 该页的其余部分具有数量不定的选项，具体取决于此处所选的目标。

![选择目标](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>选择目标
 **目标**  
 通过选择可以将数据导入到目标中的数据提供程序来指定目标。
 
-   **通常可从名称判断出所需的数据提供程序**，因为提供程序的名称通常包含目标名称，例如*平面文件*目标、Microsoft *Excel*、Microsoft *Access*、用于 *SqlServer* 的 .Net Framework 数据提供程序、用于 *Oracle* 的 .Net Framework 数据提供程序。

-   **如果有用于目标的 ODBC 驱动程序**，则选择用于 ODBC 的 .Net Framework 数据提供程序。 然后输入特定于驱动程序的信息。 目标下拉列表中不会列出 ODBC 驱动程序。 用于 ODBC 的 .Net Framework 数据提供程序充当 ODBC 驱动程序的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **可用于目标的访问接口可能不止一个。** 通常可以选择任何可用于目标的访问接口。 例如，若要连接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以使用用于 SQL Server 的 .NET Framework 数据提供程序或 SQL Server ODBC 驱动程序。 （其他提供程序也仍在列表中，但不再受支持。） 

## <a name="my-destination-isnt-in-the-list"></a>我的目标不在列表中
-   **可能需要从 Microsoft 或第三方下载数据提供程序**。 “目标”列表中的可用数据提供程序列表仅包含计算机上安装的提供程序。 有关可使用的目标的信息，请参阅[可使用哪些数据源和目标？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **是否有用于目标的 ODBC 驱动程序？** 目标下拉列表中不会列出 ODBC 驱动程序。 如果有用于目标的 ODBC 驱动程序，则选择用于 ODBC 的 .Net Framework 数据提供程序。 然后输入特定于驱动程序的信息。 用于 ODBC 的 .Net Framework 数据提供程序充当 ODBC 驱动程序的包装器。 有关详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **64 位和 32 位提供程序。** 如果运行的是 64 位向导，则看不到仅安装了 32 位提供程序的目标，反之亦然。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

## <a name="after-you-choose-a-destination"></a>选择目标之后
在选择目标之后，“选择目标”页的其余部分具有数量不定的选项，具体取决于所选的数据提供程序。

若要连接到常用目标，请参阅以下页面之一。
-   [连接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [连接到平面文件（文本文件）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 连接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 Azure Blob 存储](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [连接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [连接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

有关如何连接到此处未列出的目标的信息，请参阅 [The Connection Strings Reference](https://www.connectionstrings.com/)（连接字符串参考）。 该第三方站点包含示例连接字符串、关于数据提供程序的详细信息以及它们需要的连接信息。

## <a name="whats-next"></a>下一步是什么？  
 提供有关数据目标以及有关如何连接到它的信息之后，下一页是“指定表复制或查询” 。 在此页上，可指定要复制整个表还是仅复制特定行。 有关详细信息，请参阅 [指定表复制或查询](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


