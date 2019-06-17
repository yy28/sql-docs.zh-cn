---
title: 提取使用 IRow 单行 |Microsoft Docs
description: 正在提取适用于 SQL Server 使用 IRow 接口的 OLE DB 驱动程序的单个行
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
manager: jroth
ms.openlocfilehash: 6e9f48ba7f2472fa215b267c915900d7c616dba0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799218"
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 提取单行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IRow**接口实现 OLE DB 驱动程序中的，为 SQL Server 经过简化，可提高性能。 IRow 允许直接访问单行对象的列  。 如果预先知道命令执行的结果确实是生成单行，则 IRow 将检索该行的列  。 如果结果集包括多行，则 IRow 将只显示第一行  。  
  
 IRow 实现不允许行的任何导航  。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  IRow::Open 只支持打开 DBGUID_STREAM 和 DBGUID_NULL 对象类型  。  
  
 若要使用 ICommand::Execute 方法获得行对象，必须传递 IID_IRow  。 必须使用 IMultipleResults 接口处理多个结果集  。 IMultipleResults 支持 IRow 和 IRowset    。 IRowset 用于大容量操作  。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IRow::GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
