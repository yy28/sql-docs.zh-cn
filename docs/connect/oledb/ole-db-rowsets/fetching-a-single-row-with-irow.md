---
title: 提取具有 IRow 的单一行 |Microsoft 文档
description: 提取单个行使用用于 SQL Server 的 OLE DB 驱动程序的 IRow 接口
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 89beb28be9c1c588ed3488f2cbbd31e1b66be778
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 提取单行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **IRow**接口实现 OLE DB 驱动程序中的，为 SQL Server 简化以提高性能。 **IRow**允许直接访问的单个行对象的列。 如果您事先知道命令执行的结果将生成恰好一个行， **IRow**将检索该行的列。 如果结果集中包括多个行， **IRow**将公开仅第一行。  
  
 **IRow**实现不允许任何导航行。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  **IRow::Open**支持要打开的对象的唯一 DBGUID_STREAM 和 DBGUID_NULL 类型。  
  
 若要获取行对象使用**ICommand::Execute**方法，必须传递 IID_IRow。 **IMultipleResults**必须使用接口来处理多个结果集。 **IMultipleResults**支持**IRow**和**IRowset**。 **IRowset**用于大容量操作。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IRow::GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
