---
title: OLE DB 驱动程序中的 SQL Server 的稀疏列支持 |Microsoft 文档
description: OLE DB 驱动程序中的 SQL Server 的稀疏列支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08de456a687ffdde2889cb3bd26bd5dbfa39a5dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>OLE DB 驱动程序中的 SQL Server 的稀疏列支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 驱动程序的 SQL Server 支持稀疏列。 有关详细信息中的稀疏列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[使用稀疏列](../../../relational-databases/tables/use-sparse-columns.md)和[使用列集](../../../relational-databases/tables/use-column-sets.md)。  
  
 稀疏列支持 OLE DB 驱动程序的 SQL Server，有关详细信息[稀疏列支持&#40;OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md)。  
  
 有关演示此功能的示例应用程序的信息，请参阅[SQL Server 数据编程示例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>稀疏列和用于 SQL Server 的 OLE DB 驱动程序的用户方案  
 下表总结了为与稀疏列的 SQL Server 用户 OLE DB 驱动程序常见的用户方案：  
  
|应用场景|行为|  
|--------------|--------------|  
|**选择\*从表**或 IOpenRowset::OpenRowset。|返回不是稀疏的成员的所有列**column_set**，加上包含的所有成员的稀疏的非 null 列的值的 XML 列**column_set**。|  
|按名称引用列。|而不考虑其稀疏列状态可以引用的列或**column_set**成员身份。|  
|访问**column_set**成员通过计算的 XML 列的列。|成员的稀疏列**column_set**可以通过选择访问**column_set**按名称和可以具有值插入和更新的更新中的 XML **column_set**列。<br /><br /> 该值必须符合的架构**column_set**列。|  
|检索所有列通过 DBSCHEMA_COLUMNS 架构行集表中没有列的限制 (OLE DB) 的元数据。|个不是的成员的所有列都返回一行**column_set**。 如果表具有稀疏**column_set**，将为其返回行。<br /><br /> 请注意这不返回成员的列的元数据**column_set**。|  
|检索所有列，而不考虑稀疏性或中的成员身份的元数据**column_set**。 此操作可能返回大量的行。|调用 idbschemarowset:: DBSCHEMA_COLUMNS_EXTENDED 架构行集。|  
|检索仅是的成员的列的元数据**column_set**。 此操作可能返回大量的行。|调用 idbschemarowset:: DBSCHEMA_SPARSE_COLUMN_SET 架构行集。|  
|确定列是否为稀疏列。|参考 DBSCHEMA_COLUMNS 架构行集 (OLE DB) 的 SS_IS_SPARSE 列。|  
|确定列是否为**column_set**。|参考 DBSCHEMA_COLUMNS 架构行集的 SS_IS_COLUMN_SET 列。 或者，请查阅*dwFlags*由 IColumnsinfo::GetColumnInfo 或 DBCOLUMNFLAGS 中 IColumnsRowset::GetColumnsRowset 返回的行集返回。 有关**column_set**列，将设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET。|  
|导入和导出 bcp 具有否的表的稀疏列**column_set**。|SQL server 从以前版本的 OLE DB 驱动程序的行为方面没有变化。|  
|导入和导出 bcp 具有的表的稀疏列**column_set**。|**Column_set**是导入和导出为 XML; 相同的方式，即作为**varbinary （max)** 如果绑定作为二进制类型，或**nvarchar (max)** 如果绑定为**char**或**wchar**类型。<br /><br /> 成员的稀疏列**column_set**不会导出为不同的列; 它们仅导出的值中**column_set**。|  
|**queryout** BCP 的行为。|从以前版本的 OLE DB 驱动程序的显式命名列的 SQL server 的处理没有变化。<br /><br /> 如果应用场景涉及在具有不同架构的表之间进行导入和导出，则可能要求特殊处理。<br /><br /> 有关 BCP 的详细信息，请参阅本章后面的“针对稀疏列的大容量复制 (BCP) 支持”。|  
  
## <a name="down-level-client-behavior"></a>下级客户端行为  
 下层客户端将返回只为的不是成员的稀疏列的元数据**column_set** SQLColumns 和 DBSCHMA_COLUMNS。
  
 下级客户端可以访问成员的稀疏列**column_set**按名称和**column_set**列将为到 XML 列的可访问性[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]客户端。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>针对稀疏列的大容量复制 (BCP) 支持  
 没有为稀疏列中 OLE DB 的 BCP api 更改或**column_set**功能。  
  
 如果表具有**column_set**，稀疏列不被当作非重复列。 中的值包括所有稀疏列的值**column_set**，这作为 XML 列; 相同的方式导出，即作为**varbinary （max)** 如果绑定作为二进制类型，或**nvarchar (max)** 如果绑定为**char**或**wchar**类型)。 在导入时， **column_set**值必须符合的架构**column_set**。  
  
 有关**queryout**操作，没有显式被引用的列的处理的方式没有更改。 **column_set**列具有 XML 列相同的行为和稀疏性不起作用的处理方式上名为稀疏列。  
  
 但是，如果**queryout**使用的导出和你引用稀疏列的稀疏列集按名称的成员，无法执行直接导入同样结构化表。 这是因为 BCP 使用元数据与一致**选择\*** 导入操作并且不能以匹配**column_set**成员与此元数据的列。 若要导入**column_set**成员列单独，必须定义上引用所需的表的视图**column_set**列，并且必须执行导入操作使用视图。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/oledb-driver-for-sql-server.md)  
  
  
