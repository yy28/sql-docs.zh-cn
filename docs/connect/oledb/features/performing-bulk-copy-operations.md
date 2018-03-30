---
title: 执行大容量复制操作 |Microsoft 文档
description: 执行大容量复制操作使用的 SQL Server OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], bulk copy operations
- OLE DB Driver for SQL Server, bulk copy operations
- MSOLEDBSQL, bulk copy operations
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f1c5eaf2edc7be8e97dd1386c8b1db2a83b3946
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="performing-bulk-copy-operations"></a>执行大容量复制操作
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大容量复制功能支持将大量数据传输到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表或视图中，或从其中传出。 也可以通过指定 SELECT 语句将数据传出。 可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和操作系统的数据文件（比如 ASCII 文件）之间移动数据。 数据文件可以有不同格式；定义格式是为了对格式文件中的数据进行大容量复制。 也可以选择将数据加载到程序变量中，然后使用大容量复制函数和方法将数据传输到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 有关演示此功能的示例应用，请参阅[大容量复制数据使用 IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)。  
  
 应用程序通常按以下方式之一使用大容量复制：  
  
-   从表、视图或 Transact-SQL 语句的结果集，将数据大容量复制到以与该表或视图相同的格式存储数据的数据文件中。  
  
     这称为本机模式数据文件。  
  
-   从表、视图或 Transact-SQL 语句的结果集，将数据大容量复制到以不同于该表或视图的格式存储数据的数据文件中。  
  
     这种情况下，将创建一个单独的格式文件，用于定义每个列存储在数据文件中时的特征（数据类型、位置、长度、终止符等等）。 如果所有列均转换为字符格式，则所产生的文件称为字符模式的数据文件。  
  
-   从数据文件大容量复制到表或视图中。  
  
     如果需要，则使用格式文件确定数据文件的布局。  
  
-   将数据加载到程序变量中，然后使用大容量复制函数将数据导入表或视图中，以便一次一行执行大容量复制。  
  
 大容量复制函数使用的数据文件不必由另一个大容量复制程序创建。 任何其他系统都可以按照大容量复制的定义生成数据文件和格式文件；然后，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大容量复制程序可以使用这些文件将数据导入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中。 例如，可以将数据从电子表格导出到以制表符分隔的文件中，然后生成描述该制表符分隔文件的格式文件，之后使用大容量复制程序将此数据快速导入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中。 还可以将大容量复制所生成的数据文件导入其他应用程序中。 例如，可以使用大容量复制函数将数据从表或视图导出到以制表符分隔的文件中，然后可以将该文件加载到电子表格中。  
  
 编写应用程序以使用大容量复制函数的程序员应当遵从常规规则，以获得良好的大容量复制性能。 有关大容量复制操作中支持的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[大容量导入和导出的数据&#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 CLR 用户定义类型 (UDT) 必须绑定为二进制数据。 即使格式文件指定将 SQLCHAR 作为目标 UDT 列的数据类型，BCP 实用工具仍会将数据视为二进制。  
  
 不要对大容量复制操作使用 SET FMTONLY OFF。 SET FMTONLY OFF 可能导致大容量复制操作失败，或导致意外的结果。  
  
## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序 
 SQL Server 的 OLE DB 驱动程序实现两种方法来执行大容量复制操作与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。 第一种方法涉及使用[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)基于内存的大容量复制操作; 和第二个接口，需使用[IBCPSession](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)基于文件的大容量复制操作的接口。  
  
### <a name="using-memory-based-bulk-copy-operations"></a>使用基于内存的大容量复制操作  
 SQL Server 的 OLE DB 驱动程序实现**IRowsetFastLoad**接口以公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]基于内存的大容量复制操作。 **IRowsetFastLoad**接口实现[IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)和[IRowsetFastLoad::InsertRow](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)方法。  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>为 IRowsetFastLoad 启用会话  
 使用者通过将特定于 SQL Server 的数据源属性 SSPROP_ENABLEFASTLOAD OLE DB 驱动程序设置为 VARIANT_TRUE 通知其需求的大容量复制的 SQL Server 的 OLE DB 驱动程序。 在数据源上设置属性，与使用者为 SQL Server 会话创建 OLE DB 驱动程序。 在新的会话允许使用者访问**IRowsetFastLoad**接口。  
  
> [!NOTE]  
>  如果**IDataInitialize**接口用于初始化数据源，则需要在中设置 SSPROP_IRowsetFastLoad 属性*rgPropertySets*参数**IOpenRowset::OpenRowset**方法; 否则为调用**OpenRowset**方法将返回 E_NOINTERFACE。  
  
 启用用于大容量复制会话的会话限制用于 SQL Server 支持的接口的 OLE DB 驱动程序。 启用大容量复制的会话仅公开以下接口：  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 若要禁用的大容量复制启用行集创建并导致 OLE DB 驱动程序的 SQL Server 会话以还原到标准处理，重置为 VARIANT_FALSE 的 SSPROP_ENABLEFASTLOAD。  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad 行集  
 用于 SQL Server 成批复制行集的 OLE DB 驱动程序是只写的但它们公开允许确定的结构的使用者的接口[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表。 以下接口公开上在大容量复制启用 OLE DB 驱动程序为 SQL Server 行集：  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 提供程序特定属性 SSPROP_FASTLOADOPTIONS、 SSPROP_FASTLOADKEEPNULLS 和 SSPROP_FASTLOADKEEPIDENTITY 控制用于 SQL Server 大容量复制行集的 OLE DB 驱动程序的行为。 在指定的属性*rgProperties*的成员*rgPropertySets* **IOpenRowset**参数成员。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|列：No<br /><br /> 读/写︰ 读/写<br /><br /> 类型：VT_BOOL<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：维护使用者提供的标识值。<br /><br /> VARIANT_FALSE：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表中的标识列的值由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 生成。 为列绑定任何值适用于 SQL Server 将忽略 OLE DB 驱动程序。<br /><br /> VARIANT_TRUE：使用者绑定的取值函数可提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 标识列的值。 标识属性不接受空值，以便使用者提供了每个唯一值的列中可用**IRowsetFastLoad::Insert**调用。|  
|SSPROP_FASTLOADKEEPNULLS|列：No<br /><br /> 读/写︰ 读/写<br /><br /> 类型：VT_BOOL<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：对于有 DEFAULT 约束的列，将保持 NULL。 仅影响接受 NULL 并应用了 DEFAULT 约束的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列。<br /><br /> VARIANT_FALSE:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]插入列的默认值的 SQL Server 使用者 OLE DB 驱动程序插入的行中的列包含 NULL 时。<br /><br /> VARIANT_TRUE:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的 SQL Server 使用者 OLE DB 驱动程序插入的列包含 NULL 的行时为该列的值插入 NULL。|  
|SSPROP_FASTLOADOPTIONS|列：No<br /><br /> 读/写︰ 读/写<br /><br /> 类型：VT_BSTR<br /><br /> 默认值：无<br /><br /> 说明： 此属性是相同**-h** "*提示*[，...*n*]"的选项**bcp**实用程序。 以下字符串可以在将数据大容量复制到表中时作为选项使用。<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,...*n*]): 数据文件中的数据的排序顺序。 如果按照表的聚集索引对加载的数据文件进行排序，将会提高大容量复制性能。<br /><br /> **ROWS_PER_BATCH** = *bb*： 每批的数据的行数 (作为*bb*)。 服务器根据 *bb*值优化大容量加载。 默认情况下， **ROWS_PER_BATCH**未知。<br /><br /> **KILOBYTES_PER_BATCH** = *cc*： 数每批次 （cc) 的数据的千字节 (KB)。 默认情况下， **KILOBYTES_PER_BATCH**未知。<br /><br /> **TABLOCK**： 大容量复制操作期间获取表级锁。 由于仅在大容量复制操作期间持有锁定会减少对表的锁定争用，因此该选项极大地提高了性能。 表可以通过多个客户端同时加载如果表没有索引和**TABLOCK**指定。 默认情况下，锁定行为由表选项**表大容量加载上的锁**。<br /><br /> **CHECK_CONSTRAINTS**： 上的任何约束*table_name*批量复制操作期间检查。 默认情况下，忽略约束。<br /><br /> **FIRE_TRIGGER**:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]触发器使用行版本控制，而且将行版本存储在版本存储区中**tempdb**。 因此，即使是在启用触发器时，也可以进行大容量记录优化。 在大容量导入具有大量的行的批处理启用的触发器之前, 可能需要展开的大小**tempdb**。|  
  
### <a name="using-file-based-bulk-copy-operations"></a>使用基于文件的大容量复制操作  
 SQL Server 的 OLE DB 驱动程序实现**IBCPSession**接口以公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]基于文件的大容量复制操作。 **IBCPSession**接口实现[IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)， [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)， [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)， [IBCPSession::BCPDone](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)， [IBCPSession::BCPExec](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)， [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)， [IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)，和[IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)方法。  
  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [数据源属性&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [批量导入和导出数据 (SQL Server)](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [优化大容量导入性能](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  

