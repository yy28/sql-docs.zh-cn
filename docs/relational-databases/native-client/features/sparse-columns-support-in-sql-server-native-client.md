---
title: SQL Server Native Client 中的稀疏列支持 |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f4d77722108f82733978b5b2c778ddfbfb958c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>SQL Server Native Client 中的稀疏列支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支持稀疏列。 有关详细信息中的稀疏列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[使用稀疏列](../../../relational-databases/tables/use-sparse-columns.md)和[使用列集](../../../relational-databases/tables/use-column-sets.md)。  
  
 有关稀疏列的详细信息，支持在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端，请参阅[稀疏列支持&#40;ODBC&#41; ](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)和[稀疏列支持&#40;OLE DB&#41; ](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md).  
  
 有关演示此功能的示例应用程序的信息，请参阅[SQL Server 数据编程示例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>稀疏列和 SQL Server Native Client 的用户应用场景  
 下表为具有稀疏列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 用户总结了常见用户应用场景：  
  
|应用场景|行为|  
|--------------|--------------|  
|**选择\*从表**或 IOpenRowset::OpenRowset。|返回不是稀疏的成员的所有列**column_set**，加上包含的所有成员的稀疏的非 null 列的值的 XML 列**column_set**。|  
|按名称引用列。|而不考虑其稀疏列状态可以引用的列或**column_set**成员身份。|  
|访问**column_set**成员通过计算的 XML 列的列。|成员的稀疏列**column_set**可以通过选择访问**column_set**按名称和可以具有值插入和更新的更新中的 XML **column_set**列。<br /><br /> 该值必须符合的架构**column_set**列。|  
|检索通过 SQLColumns 具有 NULL 或 %(ODBC); 列搜索模式的表中的所有列的元数据或通过无列限制 (OLE DB) DBSCHEMA_COLUMNS 架构行集。|个不是的成员的所有列都返回一行**column_set**。 如果表具有稀疏**column_set**，将为其返回行。<br /><br /> 请注意这不返回成员的列的元数据**column_set**。|  
|检索所有列，而不考虑稀疏性或中的成员身份的元数据**column_set**。 此操作可能返回大量的行。|将描述符字段 SQL_SOPT_SS_NAME_SCOPE 设置为 SQL_SS_NAME_SCOPE_EXTENDED 并调用[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC)。<br /><br /> 调用 idbschemarowset:: DBSCHEMA_COLUMNS_EXTENDED 架构行集 (OLE DB)。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，这样的应用程序可以直接查询系统视图。|  
|检索仅是的成员的列的元数据**column_set**。 此操作可能返回大量的行。|将描述符字段 SQL_SOPT_SS_NAME_SCOPE 设置为 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 并调用 SQLColumns (ODBC)。<br /><br /> 调用 idbschemarowset:: DBSCHEMA_SPARSE_COLUMN_SET 架构行集 (OLE DB)。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以查询系统视图。|  
|确定列是否为稀疏列。|请查阅 SQLColumns 结果集 (ODBC) 的 SS_IS_SPARSE 列。<br /><br /> 参考 DBSCHEMA_COLUMNS 架构行集 (OLE DB) 的 SS_IS_SPARSE 列。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以查询系统视图。|  
|确定列是否为**column_set**。|请查阅 SQLColumns 结果集的 SS_IS_COLUMN_SET 列。 或者，参考特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的列属性 SQL_CA_SS_IS_COLUMN_SET (ODBC)。<br /><br /> 参考 DBSCHEMA_COLUMNS 架构行集的 SS_IS_COLUMN_SET 列。 或者，请查阅*dwFlags*由 IColumnsinfo::GetColumnInfo 或 DBCOLUMNFLAGS 中 IColumnsRowset::GetColumnsRowset 返回的行集返回。 有关**column_set**列，DBCOLUMNFLAGS_SS_ISCOLUMNSET 将设置 (OLE DB)。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以查询系统视图。|  
|导入和导出 bcp 具有否的表的稀疏列**column_set**。|在行为上与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的以前版本相比没有变化。|  
|导入和导出 bcp 具有的表的稀疏列**column_set**。|**Column_set**是导入和导出为 XML; 相同的方式，即作为**varbinary （max)**如果绑定作为二进制类型，或**nvarchar (max)**如果绑定为**char**或**wchar**类型。<br /><br /> 成员的稀疏列**column_set**不会导出为不同的列; 它们仅导出的值中**column_set**。|  
|**queryout** BCP 的行为。|在处理显式命名的列上与以前版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 相比没有变化。<br /><br /> 如果应用场景涉及在具有不同架构的表之间进行导入和导出，则可能要求特殊处理。<br /><br /> 有关 BCP 的详细信息，请参阅本章后面的“针对稀疏列的大容量复制 (BCP) 支持”。|  
  
## <a name="down-level-client-behavior"></a>下级客户端行为  
 下层客户端将返回只为的不是成员的稀疏列的元数据**column_set** SQLColumns 和 DBSCHMA_COLUMNS。 中引入的其他 OLE DB 架构行集[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]本机客户端将不可用，也不会对 SQLColumns 通过 SQL_SOPT_SS_NAME_SCOPE ODBC 中进行修改。  
  
 下级客户端可以访问成员的稀疏列**column_set**按名称和**column_set**列将为到 XML 列的可访问性[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]客户端。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>针对稀疏列的大容量复制 (BCP) 支持  
 没有为稀疏列中 ODBC 或 OLE DB 的 BCP api 更改或**column_set**功能。  
  
 如果表具有**column_set**，稀疏列不被当作非重复列。 中的值包括所有稀疏列的值**column_set**，这作为 XML 列; 相同的方式导出，即作为**varbinary （max)**如果绑定作为二进制类型，或**nvarchar (max)**如果绑定为**char**或**wchar**类型)。 在导入时， **column_set**值必须符合的架构**column_set**。  
  
 有关**queryout**操作，没有显式被引用的列的处理的方式没有更改。 **column_set**列具有 XML 列相同的行为和稀疏性不起作用的处理方式上名为稀疏列。  
  
 但是，如果**queryout**使用的导出和你引用稀疏列的稀疏列集按名称的成员，无法执行直接导入同样结构化表。 这是因为 BCP 使用元数据与一致**选择\***导入操作并且不能以匹配**column_set**成员与此元数据的列。 若要导入**column_set**成员列单独，必须定义上引用所需的表的视图**column_set**列，并且必须执行导入操作使用视图。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
