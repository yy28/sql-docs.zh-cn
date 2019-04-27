---
title: SQL Server Native Client 中的稀疏列支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e21bd33bd181dc4075b74256047336562d11fb4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744428"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>SQL Server Native Client 中的稀疏列支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支持稀疏列。 有关中的稀疏列的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[使用稀疏列](../../../relational-databases/tables/use-sparse-columns.md)并[使用列集](../../../relational-databases/tables/use-column-sets.md)。  
  
 有关稀疏列支持在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client，请参阅[稀疏列支持&#40;ODBC&#41; ](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)并[稀疏列支持&#40;OLE DB&#41; ](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md).  
  
 有关演示此功能的示例应用程序的信息，请参阅 [SQL Server 数据编程示例](https://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>稀疏列和 SQL Server Native Client 的用户应用场景  
 下表为具有稀疏列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 用户总结了常见用户应用场景：  
  
|应用场景|行为|  
|--------------|--------------|  
|**选择\*从表**或 iopenrowset:: Openrowset。|返回不是稀疏 column_set 的成员的所有列，以及包含是稀疏 column_set 的成员的所有非空列值的 XML 列。|  
|按名称引用列。|可以不考虑其稀疏列状态或 column_set 成员身份如何而引用列。|  
|通过计算的 XML 列访问 column_set 成员列。|作为稀疏 column_set 的成员的列可以通过按名称选择 column_set 进行访问，并且可通过在 column_set 列中更新 XML 插入和更新值。<br /><br /> 该值必须符合针对 column_set 列的架构。|  
|检索与列搜索模式的为 NULL 或 %(ODBC); 通过 SQLColumns 表中的所有列的元数据或通过不含列限制 (OLE DB) 的 DBSCHEMA_COLUMNS 架构行集。|为不是 column_set 的成员的所有列返回行。 如果该表具有稀疏 column_set，则将为其返回一行。<br /><br /> 请注意，此操作并不返回是 column_set 的成员的列的元数据。|  
|检索所有列的元数据，而不管 column_set 中的稀疏性或成员身份如何。 此操作可能返回大量的行。|将描述符字段 sql_sopt_ss_name_scope 设置为 SQL_SS_NAME_SCOPE_EXTENDED 并且调用[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC)。<br /><br /> 为 DBSCHEMA_COLUMNS_EXTENDED 架构行集 (OLE DB) 调用 idbschemarowset:: Getrowset。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以直接查询系统视图。|  
|只为是 column_set 成员的列检索元数据。 此操作可能返回大量的行。|设置描述符字段 sql_sopt_ss_name_scope 设置为 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 并且调用 SQLColumns (ODBC)。<br /><br /> 为 DBSCHEMA_SPARSE_COLUMN_SET 架构行集 (OLE DB) 调用 idbschemarowset:: Getrowset。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以查询系统视图。|  
|确定列是否为稀疏列。|请查阅 SQLColumns 结果集 (ODBC) 的 SS_IS_SPARSE 列。<br /><br /> 参考 DBSCHEMA_COLUMNS 架构行集 (OLE DB) 的 SS_IS_SPARSE 列。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以查询系统视图。|  
|确定列是否**column_set**。|请查阅 SQLColumns 结果集的 SS_IS_COLUMN_SET 列。 或者，参考特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的列属性 SQL_CA_SS_IS_COLUMN_SET (ODBC)。<br /><br /> 参考 DBSCHEMA_COLUMNS 架构行集的 SS_IS_COLUMN_SET 列。 或者，参考*dwFlags*由 icolumnsinfo:: Getcolumninfo 或 DBCOLUMNFLAGS 中 icolumnsrowset:: Getcolumnsrowset 返回的行集返回。 有关**column_set**列，将设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET (OLE DB)。<br /><br /> 如果应用程序使用来自早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本中的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client，则此应用场景不可行。 但是，此类应用程序可以查询系统视图。|  
|为没有 column_set 的表按 BCP 导入和导出稀疏列。|在行为上与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的以前版本相比没有变化。|  
|为有 column_set 的表按 BCP 导入和导出稀疏列。|**Column_set**导入和导出为 XML; 相同的方式，即作为**varbinary （max)** 如果绑定为二进制类型，或与**nvarchar （max)** 如果绑定为**char**或**wchar**类型。<br /><br /> 是稀疏 column_set 的成员的列不导出为非重复列；它们只导出在 column_set 的值中。|  
|**queryout** BCP 的行为。|在处理显式命名的列上与以前版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 相比没有变化。<br /><br /> 如果应用场景涉及在具有不同架构的表之间进行导入和导出，则可能要求特殊处理。<br /><br /> 有关 BCP 的详细信息，请参阅本章后面的“针对稀疏列的大容量复制 (BCP) 支持”。|  
  
## <a name="down-level-client-behavior"></a>下级客户端行为  
 下级客户端将只为不属于 SQLColumns 和 DBSCHMA_COLUMNS 的稀疏 column_set 的成员的列返回元数据。 中引入的其他 OLE DB 架构行集[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]本机客户端将不可用，也不会在通过 SQL_SOPT_SS_NAME_SCOPE ODBC SQLColumns 对的修改。  
  
 下级客户端将按名称访问作为稀疏 column_set 的成员的列，并且 column_set 列将可作为 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 客户端的 XML 列访问。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>针对稀疏列的大容量复制 (BCP) 支持  
 没有为稀疏列 ODBC 或 OLE DB 中的 BCP api 的更改或**column_set**功能。  
  
 如果某一表具有 column_set，则稀疏列不作为非重复列处理。 值中包含的所有稀疏列的值**column_set**，这导出为 XML 列; 相同的方式，即作为**varbinary （max)** 如果绑定为二进制类型，或与**nvarchar （max)** 如果绑定为**char**或**wchar**类型)。 在导入时， **column_set**值必须符合的架构**column_set**。  
  
 对于 queryout 操作，在处理显式引用的列的方式上没有变化。 column_set 列具有与 XML 列相同的行为，并且稀疏性对于命名稀疏列的处理没有影响。  
  
 但是，如果 queryout 用于导出并且引用的稀疏列属于按名称的稀疏列集的成员，则不能执行向类似结构表的直接导入。 这是因为 BCP 使用元数据与一致**选择&#42;** 导入操作并且不能以匹配**column_set**成员列与此元数据。 若要单独导入 column_set 成员列，必须对引用所需 column_set 列的表定义一个视图，并且必须使用该视图执行导入操作。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
