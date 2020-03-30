---
title: 使用 IRow 提取单行 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 的 IRow 接口提取单行
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 542875dc322cd94970c238747db0adb139b9a480
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994291"
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 提取单行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 中的 IRow  接口实现得以简化，以提高性能。 IRow 允许直接访问单行对象的列  。 如果预先知道命令执行的结果确实是生成单行，则 IRow 将检索该行的列  。 如果结果集包括多行，则 IRow 将只显示第一行  。  
  
 IRow 实现不允许行的任何导航  。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  IRow::Open 只支持打开 DBGUID_STREAM 和 DBGUID_NULL 对象类型  。  
  
 若要使用 ICommand::Execute 方法获得行对象，必须传递 IID_IRow  。 必须使用 IMultipleResults 接口处理多个结果集  。 IMultipleResults 支持 IRow 和 IRowset    。 IRowset 用于大容量操作  。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IRow::GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
