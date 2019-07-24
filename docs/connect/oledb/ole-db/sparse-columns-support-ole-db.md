---
title: 稀疏列支持 (OLE DB) |Microsoft Docs
description: 稀疏列支持 (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 701b2d9e7a6d51b7fa13f797c6c5c9de75bed5d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993857"
---
# <a name="sparse-columns-support-ole-db"></a>稀疏列支持 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主题提供有关针对稀疏列的 SQL Server 支持 OLE DB 驱动程序的信息。 有关稀疏列的详细信息, 请参阅[SQL Server OLE DB 驱动程序中的稀疏列支持](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)。 例如，请参阅[显示稀疏列的列和目录元数据 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 语句元数据  
 从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 开始，可以使用新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET。 应当为是 column_set 值的列设置该值  。 可以通过 IColumnsInfo:: GetColumnsInfo 的*dwFlags*参数和 DBCOLUMN_FLAGS:: IColumnsRowset 返回的行集的 GetColumnsRowset 列来检索 DBCOLUMNFLAGS 标志。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 目录元数据  
 其他两个特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的列已添加到 DBSCHEMA_COLUMNS 中。  
  
|列名|数据类型|值/注释|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|如果该列是稀疏列，它将具有值 VARIANT_TRUE；否则，为 VARIANT_FALSE。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|如果该列是稀疏 column_set 列，则它具有值 VARIANT_TRUE；否则，为 VARIANT_FALSE  。|  
  
 还添加了其他两个架构行集。 这些行集具有与 DBSCHEMA_COLUMNS 相同的结构，但返回不同内容。 不管 column_set 成员身份是什么，DBSCHEMA_COLUMNS_EXTENDED 都将返回所有列  。 DBSCHEMA_SPARSE_COLUMN_SET 仅返回属于稀疏 column_set 的成员的列  。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 行为  
 **DataTypeCompatibility = 80** (在连接字符串中) 的行为与[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]客户端一致, 如下所示:  
  
-   新架构行集是不可见的，并且在架构行集中没有它们的行。  
  
-   COLUMNS 行集中的新列是不可见的。  
  
-   不为 column_set 列设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET  。  
  
-   为 column_set 列设置 DBCOMPUTEMODE_NOTCOMPUTED  。  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB 对稀疏列的支持  
 以下 OLE DB 接口已在 SQL Server 的 OLE DB 驱动程序中进行了修改以支持稀疏列:  
  
|类型或成员函数|描述|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|为 dwFlags 中的 column_set 列设置了新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET   。<br /><br /> 为 column_set 列设置了 DBCOLUMNFLAGS_WRITE  。|  
|IColumsRowset::GetColumnsRowset|为 DBCOLUMN_FLAGS 中的 column_set 列设置了新的 DBCOLUMNFLAGS 标记值 DBCOLUMNFLAGS_SS_ISCOLUMNSET  。<br /><br /> 对于 column_set 列，将 DBCOLUMN_COMPUTEMODE 设置为 DBCOMPUTEMODE_DYNAMIC  。|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS 返回两个新列：SS_IS_COLUMN_SET 和 SS_IS_SPARSE。<br /><br /> DBSCHEMA_COLUMNS 仅返回不属于 column_set 成员的列  。<br /><br /> 已添加两个新架构行集：不管 column_set 成员身份的稀疏性如何，DBSCHEMA_COLUMNS_EXTENDED 都将返回所有列  。 DBSCHEMA_SPARSE_COLUMN_SET 仅返回属于 column_set 成员的列  。 这些新行集具有与 DBSCHEMA_COLUMNS 相同的列和限制。|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas 将新行集 DBSCHEMA_COLUMNS_EXTENDED 和 DBSCHEMA_SPARSE_COLUMN_SET 的 GUID 包括在可用架构行集的列表中。|  
|ICommand::Execute|如果使用从表中选择 \*，它将返回不属于稀疏 column_set 成员的所有列，外加一个 XML 列（如果有），其中包含属于稀疏 column_set 成员的所有非 NULL 列的值     。|  
|IOpenRowset::OpenRowset|IOpenRowset:: OpenRowset 返回具有与 ICommand:: Execute 相同的列的行集, 并在同一个表中使用**select \*** 查询。|  
|ITableDefinition|对于稀疏列或 column_set 列，该接口没有更改  。 必须进行架构修改的应用程序必须直接执行正确的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。|  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
