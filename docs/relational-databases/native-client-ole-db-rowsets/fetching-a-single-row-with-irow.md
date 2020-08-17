---
description: '使用 IRow (Native Client OLE DB 提供程序提取单行) '
title: 通过 IRow (Native Client OLE DB 提供程序获取单行) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e89b550533363e6526b0ce9a2affd02d1d8bc71c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88327823"
---
# <a name="fetching-a-single-row-with-irow-native-client-ole-db-provider"></a>使用 IRow (Native Client OLE DB 提供程序提取单行) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  OLE DB 提供程序中的 **IRow** 接口实现进行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 了简化，以提高性能。 IRow 允许直接访问单行对象的列  。 如果预先知道命令执行的结果确实是生成单行，则 IRow 将检索该行的列  。 如果结果集包括多行，则 IRow 将只显示第一行  。  
  
 IRow 实现不允许行的任何导航  。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  IRow::Open 只支持打开 DBGUID_STREAM 和 DBGUID_NULL 对象类型  。  
  
 若要使用 ICommand::Execute 方法获得行对象，必须传递 IID_IRow  。 必须使用 IMultipleResults 接口处理多个结果集  。 IMultipleResults 支持 IRow 和 IRowset    。 IRowset 用于大容量操作  。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IRow::GetColumns](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [使用 IRow 提取 BLOB 数据](https://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
