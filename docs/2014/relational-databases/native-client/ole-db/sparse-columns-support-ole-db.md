---
title: 稀疏列支持 (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bce02bc96e47ac824d1e95c86abaa6fcf47fef21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126844"
---
# <a name="sparse-columns-support-ole-db"></a>稀疏列支持 (OLE DB)
  本主题提供有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 对稀疏列的支持的信息。 有关稀疏列的详细信息，请参阅[中 SQL Server Native Client 的稀疏列支持](../features/sparse-columns-support-in-sql-server-native-client.md)。 有关示例，请参阅[显示列和稀疏列的目录元数据&#40;OLE DB&#41;](../../native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 语句元数据  
 从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 开始，可以使用新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET。 应当为是 `column_set` 值的列设置该值。 可以通过检索 DBCOLUMNFLAGS 标志*dwFlags* IColumnsInfo::GetColumnsInfo 和 IColumnsRowset::GetColumnsRowset 返回的行集的 DBCOLUMN_FLAGS 列参数。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 目录元数据  
 其他两个特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的列已添加到 DBSCHEMA_COLUMNS 中。  
  
|列名|数据类型|值/注释|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|如果该列是稀疏列，它将具有值 VARIANT_TRUE；否则，为 VARIANT_FALSE。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|如果该列是稀疏 `column_set` 列，则它具有值 VARIANT_TRUE；否则，为 VARIANT_FALSE。|  
  
 还添加了其他两个架构行集。 这些行集具有与 DBSCHEMA_COLUMNS 相同的结构，但返回不同内容。 不管 `column_set` 成员身份是什么，DBSCHEMA_COLUMNS_EXTENDED 都将返回所有列。 DBSCHEMA_SPARSE_COLUMN_SET 仅返回属于稀疏 `column_set` 的成员的列。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 行为  
 在 `DataTypeCompatibility=80` 时（在连接字符串中）的行为与 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 客户端一致，如下所示：  
  
-   新架构行集是不可见的，并且在架构行集中没有它们的行。  
  
-   COLUMNS 行集中的新列是不可见的。  
  
-   不为 `column_set` 列设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET。  
  
-   为 `column_set` 列设置 DBCOMPUTEMODE_NOTCOMPUTED。  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB 对稀疏列的支持  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中修改了以下 OLE DB 接口以支持稀疏列：  
  
|类型或成员函数|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|新 DBCOLUMNFLAGS 标志 DBCOLUMNFLAGS_SS_ISCOLUMNSET 设置为值`column_set`中的列*dwFlags*。<br /><br /> 为 `column_set` 列设置了 DBCOLUMNFLAGS_WRITE。|  
|IColumsRowset::GetColumnsRowset|为 DBCOLUMN_FLAGS 中的 `column_set` 列设置了新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET。<br /><br /> 对于 `column_set` 列，将 DBCOLUMN_COMPUTEMODE 设置为 DBCOMPUTEMODE_DYNAMIC。|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS 返回两个新列：SS_IS_COLUMN_SET 和 SS_IS_SPARSE。<br /><br /> DBSCHEMA_COLUMNS 仅返回不属于 `column_set` 成员的列。<br /><br /> 已添加两个新架构行集：不管 `column_set` 成员身份的稀疏性如何，DBSCHEMA_COLUMNS_EXTENDED 都将返回所有列。 DBSCHEMA_SPARSE_COLUMN_SET 仅返回属于 `column_set` 成员的列。 这些新行集具有与 DBSCHEMA_COLUMNS 相同的列和限制。|  
|IDBSchemaRowset::GetSchemas|Idbschemarowset:: Getschemas 可用架构行集的列表中包括 DBSCHEMA_COLUMNS_EXTENDED 和 DBSCHEMA_SPARSE_COLUMN_SET 的新行集的 Guid。|  
|ICommand::Execute|如果**选择\*从***表*是使用，它将返回不是稀疏的成员的所有列`column_set`，加上包含的所有非 null 列的值的 XML 列成员的稀疏`column_set`，如果存在。|  
|IOpenRowset::OpenRowset|IOpenRowset::OpenRowset 返回作为 ICommand::Execute，相同的列行集**选择\*** 对同一个表的查询。|  
|ITableDefinition|对于稀疏列或 `column_set` 列，该接口没有更改。 必须进行架构修改的应用程序必须直接执行正确的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](sql-server-native-client-ole-db.md)  
  
  