---
title: 稀疏列支持 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 25e45c61290a45240d5e4595a015b543ed89db29
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409096"
---
# <a name="sparse-columns-support-ole-db"></a>稀疏列支持 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题提供有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 对稀疏列的支持的信息。 有关稀疏列的详细信息，请参阅[SQL Server Native Client 中的稀疏列支持](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。 有关示例，请参阅[显示列和目录元数据对稀疏列&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 语句元数据  
 从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 开始，可以使用新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET。 此值应设置为的列**column_set**值。 可以通过检索 DBCOLUMNFLAGS 标记*dwFlags* icolumnsinfo:: Getcolumnsinfo 和 icolumnsrowset:: Getcolumnsrowset 返回的行集的 DBCOLUMN_FLAGS 列的参数。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 目录元数据  
 其他两个特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的列已添加到 DBSCHEMA_COLUMNS 中。  
  
|列名|数据类型|值/注释|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|如果该列是稀疏列，它将具有值 VARIANT_TRUE；否则，为 VARIANT_FALSE。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|如果列是稀疏**column_set**列中，它将具有值 VARIANT_TRUE; 否则为 VARIANT_FALSE。|  
  
 还添加了其他两个架构行集。 这些行集具有与 DBSCHEMA_COLUMNS 相同的结构，但返回不同内容。 DBSCHEMA_COLUMNS_EXTENDED 返回所有列而不考虑**column_set**成员身份。 DBSCHEMA_SPARSE_COLUMN_SET 返回成员的稀疏的列**column_set**。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 行为  
 与行为**DataTypeCompatibility = 80** （在连接字符串中） 是符合[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]客户端，按如下所示：  
  
-   新架构行集是不可见的，并且在架构行集中没有它们的行。  
  
-   COLUMNS 行集中的新列是不可见的。  
  
-   未设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET **column_set**列。  
  
-   有关设置 DBCOMPUTEMODE_NOTCOMPUTED **column_set**列。  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB 对稀疏列的支持  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中修改了以下 OLE DB 接口以支持稀疏列：  
  
|类型或成员函数|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|新的 DBCOLUMNFLAGS 标记的值的设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET **column_set**中的列*dwFlags*。<br /><br /> 为设置了 DBCOLUMNFLAGS_WRITE **column_set**列。|  
|IColumsRowset::GetColumnsRowset|为设置新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET **column_set** DBCOLUMN_FLAGS 中的列。<br /><br /> DBCOLUMN_COMPUTEMODE 设置为 DBCOMPUTEMODE_DYNAMIC **column_set**列。|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS 返回两个新列：SS_IS_COLUMN_SET 和 SS_IS_SPARSE。<br /><br /> DBSCHEMA_COLUMNS 返回不是的成员的列**column_set**。<br /><br /> 已添加两个新的架构行集： DBSCHEMA_COLUMNS_EXTENDED 都将返回所有列的稀疏性无论**column_set**成员身份。 DBSCHEMA_SPARSE_COLUMN_SET 返回的成员的列**column_set**。 这些新行集具有与 DBSCHEMA_COLUMNS 相同的列和限制。|  
|IDBSchemaRowset::GetSchemas|Idbschemarowset:: Getschemas 可用架构行集的列表中包括的新行集 DBSCHEMA_COLUMNS_EXTENDED 和 DBSCHEMA_SPARSE_COLUMN_SET 的 Guid。|  
|ICommand::Execute|如果**选择\*从***表*是使用，它将返回所有列的不是成员的稀疏**column_set**，外加一个 XML 列，其中包含的所有值非 null 列成员的稀疏**column_set**，如果存在。|  
|IOpenRowset::OpenRowset|Iopenrowset:: Openrowset 使用 icommand:: Execute，与相同的列的行集返回与**选择\*** 同一个表的查询。|  
|ITableDefinition|没有为稀疏列或此接口没有更改**column_set**列。 必须进行架构修改的应用程序必须直接执行正确的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
