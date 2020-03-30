---
title: 指定表复制或查询（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f561fd0e5817ecc03e8d5fe4cc8c32661ebdca21
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296242"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>指定表复制或查询（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  提供有关数据目标以及有关如何连接到它的信息之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“指定表复制或查询”  。 在此页上，可选择以下选项之一。
-   **复制一个或多个表或视图的数据**。 想要从列表中选取一个或多个表。
-   **编写查询以指定要传输的数据**。 想要在 SQL 查询的文本中输入或粘贴。
    
> [!TIP]
> 如果必须复制多个数据库或数据库对象（而非表和视图），请使用复制数据库向导，而不是使用导入和导出向导。 有关详细信息，请参阅 [使用复制数据库向导](../../relational-databases/databases/use-the-copy-database-wizard.md)。     
 
## <a name="screen-shot-of-the-specify-table-copy-or-query-page"></a>“指定表复制或查询”页的屏幕截图    
 以下屏幕截图显示向导的“指定表复制或查询”  页。    
    
 ![导入和导出向导的表复制或查询页](../../integration-services/import-export-data/media/table-copy-or-query.png "导入和导出向导的表复制或查询页")    
    
## <a name="specify-whether-to-copy-an-entire-table-or-write-a-query"></a>指定是否复制整个表或编写查询 
 **复制一个或多个表或视图的数据**    
 如果要在不对记录进行筛选或排序的情况下复制源中的数据，请选择此选项。   

选择“复制一个或多个表或视图的数据  时，可以从一个表或视图复制到一个目标表，或从多个表或视图复制到多个目标表。

 单击后“下一步”  之后，在“选择源表和源视图”  页上选择要复制的表。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。   
    
 **编写查询以指定要传输的数据**    
 如果要在将源数据复制到目标之前对其进行筛选或排序，请选择此选项。    
    
选择“编写查询以指定要传输的数据”  时，可以只将一个查询的结果复制到一个目标表。  

单击后“下一步”  之后，在“提供源查询”  对话框中提供 SQL 语句以指定列并选择行。 有关详细信息，请参阅 [提供源查询](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)。   
    
## <a name="why-isnt-the-copy-option-available"></a>为何复制选项不可用？    
 当向导使用 **数据提供程序连接到数据源时，“复制一个或多个表或视图的数据”** [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 选项可能不可用。 当向导没有关于数据提供程序的足够信息用于从数据源请求表和视图列表时，会发生这种情况。 
 
只要知道要导出的表的名称，仍可使用“编写查询”选项，即便通常不编写 SQL 查询也是如此  。 在“提供源查询”对话框（单击“下一步”后看到）中，以 `SELECT * FROM <name of table>` 形式输入查询   。 如果表名称包含空格或其他特殊字符，使用方括号将名称括起来，如 `SELECT * FROM [<name of table>]`。

### <a name="more-info"></a>更多信息
 “复制一个或多个表或视图的数据”  选项仅对在 ProviderDescriptors.xml 文件中有 ProviderDescription 部分的信息的那些访问接口可用。 （默认情况下，此文件位于 \<drive>:\Program Files\Microsoft SQL Server\130\DTS\ProviderDescriptors 中  。）此文件中的每个 ProviderDescription 部分都包含从相应访问接口检索元数据所需的信息。    
    
 默认情况下，ProviderDescriptors.xml 文件仅包含用于以下列表中的访问接口的 ProviderDescription 部分。    
    
-   用于 SQL Server 的 .NET Framework 数据访问接口 (System.Data.SqlClient)    
    
-   用于 Oracle 的 .NET Framework 数据访问接口 (System.Data.OracleClient)    
    
-   用于 ODBC 的 .NET Framework 数据访问接口 (System.Data.Odbc)    
    
-    System.Data.OleDb（适用于所有 OLE DB 访问接口）    
    
-   通过 Microsoft Host Integration Server 安装的 Microsoft Provider for DB2 (Microsoft.HostIntegration.MsDb2Client.MsDb2Connection)    
    
 第三方开发人员可以向 ProviderDescriptors.xml 文件添加 ProviderDescriptor 部分，从而使其访问接口可以使用“复制一个或多个表或视图的数据”  选项。 若要查看 ProviderDescriptor 部分的要求，请参阅 ProviderDescriptors.xsd 架构文件，默认情况下，该文件位于 ProviderDescriptors.xml 文件所在的文件夹中。    
    
## <a name="whats-next"></a>下一步是什么？    
 指定是要复制整个表还是提供查询之后，下一页取决于在此页上选择的选项以及数据的目标。    
    
-   如果选择了“复制一个或多个表或视图的数据”  ，则对于大多数目标，下一页是“选择源表和源视图”  。 在此页上，可选择现有表和视图以从数据源复制到目标。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。    
    
-   如果选择了“复制一个或多个表或视图的数据”  并且目标是平面文件，则下一页是“配置平面文件目标”  。 在此页上，可为目标平面文件指定格式设置选项。 （随后在配置平面文件之后，下一页是“选择源表和源视图”  。）有关详细信息，请参阅[配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。    
    
-   如果选择了“编写查询以指定要传输的数据”  ，则下一页是“提供源查询”  。 在此页上，可编写并测试选择要从数据源复制到目标的数据的 SQL 语句。 （随后在提供查询之后，下一页是“选择源表和源视图”  。）有关详细信息，请参阅[提供源查询](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)。

## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


