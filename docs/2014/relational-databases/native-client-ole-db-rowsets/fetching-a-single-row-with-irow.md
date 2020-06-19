---
title: 使用 IRow 提取单行 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b5573fe1fef39f29329e373323f5f8aaf15f2c58
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055957"
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 提取单行
  OLE DB 提供程序中的**IRow**接口实现进行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 了简化，以提高性能。 IRow 允许直接访问单行对象的列****。 如果预先知道命令执行的结果确实是生成单行，则 IRow 将检索该行的列****。 如果结果集包括多行，则 IRow 将只显示第一行****。  
  
 IRow 实现不允许行的任何导航****。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  IRow::Open 只支持打开 DBGUID_STREAM 和 DBGUID_NULL 对象类型****。  
  
 若要使用 ICommand::Execute 方法获得行对象，必须传递 IID_IRow****。 必须使用 IMultipleResults 接口处理多个结果集****。 IMultipleResults 支持 IRow 和 IRowset************。 IRowset 用于大容量操作****。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [使用 IRow 提取 BLOB 数据](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>另请参阅  
 [行集](rowsets.md)  
  
  
