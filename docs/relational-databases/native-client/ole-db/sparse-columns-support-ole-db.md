---
title: "稀疏列支持 (OLE DB) |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83781fb2194f5ef94ea7a73a8c32017ceb25424a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="sparse-columns-support-ole-db"></a>稀疏列支持 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主题提供有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 对稀疏列的支持的信息。 有关稀疏列的详细信息，请参阅[中 SQL Server Native Client 的稀疏列支持](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。 有关示例，请参阅[显示列和稀疏列 &#40; OLE DB &#41; 的目录元数据](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 语句元数据  
 从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 开始，可以使用新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET。 此值应为列都设置**column_set**值。 可以通过检索 DBCOLUMNFLAGS 标志*dwFlags* IColumnsInfo::GetColumnsInfo 和 IColumnsRowset::GetColumnsRowset 返回的行集的 DBCOLUMN_FLAGS 列参数。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 目录元数据  
 其他两个特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的列已添加到 DBSCHEMA_COLUMNS 中。  
  
|列名|数据类型|值/注释|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|如果该列是稀疏列，它将具有值 VARIANT_TRUE；否则，为 VARIANT_FALSE。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|如果列是稀疏**column_set**列，则此项的值 VARIANT_TRUE; 否则为 VARIANT_FALSE。|  
  
 还添加了其他两个架构行集。 这些行集具有与 DBSCHEMA_COLUMNS 相同的结构，但返回不同内容。 DBSCHEMA_COLUMNS_EXTENDED 返回而不考虑所有列**column_set**成员身份。 DBSCHEMA_SPARSE_COLUMN_SET 返回成员的稀疏的列**column_set**。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 行为  
 与行为**DataTypeCompatibility = 80** （在连接字符串中） 是与一致[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]客户端，，如下所示：  
  
-   新架构行集是不可见的，并且在架构行集中没有它们的行。  
  
-   COLUMNS 行集中的新列是不可见的。  
  
-   没有为设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET **column_set**列。  
  
-   为设置 DBCOMPUTEMODE_NOTCOMPUTED **column_set**列。  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB 对稀疏列的支持  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中修改了以下 OLE DB 接口以支持稀疏列：  
  
|类型或成员函数|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|新 DBCOLUMNFLAGS 标志 DBCOLUMNFLAGS_SS_ISCOLUMNSET 设置为值**column_set**中的列*dwFlags*。<br /><br /> 为设置 DBCOLUMNFLAGS_WRITE **column_set**列。|  
|IColumsRowset::GetColumnsRowset|为设置新 DBCOLUMNFLAGS 标志值，DBCOLUMNFLAGS_SS_ISCOLUMNSET， **column_set** DBCOLUMN_FLAGS 中的列。<br /><br /> DBCOLUMN_COMPUTEMODE 设置为 DBCOMPUTEMODE_DYNAMIC 为**column_set**列。|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS 返回两个新列：SS_IS_COLUMN_SET 和 SS_IS_SPARSE。<br /><br /> DBSCHEMA_COLUMNS 返回不是的成员的列**column_set**。<br /><br /> 已添加两个新的架构行集： DBSCHEMA_COLUMNS_EXTENDED 将返回所有列的稀疏性无论**column_set**成员身份。 DBSCHEMA_SPARSE_COLUMN_SET 返回的成员的列**column_set**。 这些新行集具有与 DBSCHEMA_COLUMNS 相同的列和限制。|  
|IDBSchemaRowset::GetSchemas|Idbschemarowset:: Getschemas 可用架构行集的列表中包括 DBSCHEMA_COLUMNS_EXTENDED 和 DBSCHEMA_SPARSE_COLUMN_SET 的新行集的 Guid。|  
|ICommand::Execute|如果**选择\*从***表*是使用，它将返回不是稀疏的成员的所有列**column_set**，加上包含的所有值的 XML 列成员的稀疏的非 null 列**column_set**，如果存在。|  
|IOpenRowset::OpenRowset|IOpenRowset::OpenRowset 返回作为 ICommand::Execute，相同的列行集**选择\***对同一个表的查询。|  
|ITableDefinition|没有此接口为稀疏列或没有更改**column_set**列。 必须进行架构修改的应用程序必须直接执行正确的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
