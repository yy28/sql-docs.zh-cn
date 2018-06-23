---
title: 提取具有 IRow 的单一行 |Microsoft 文档
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
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eef27a6cbd6ee793cd227c2cf6e6570e1d04b004
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126070"
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 提取单行
  **IRow**接口中的实现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]简化 Native Client OLE DB 提供程序以提高性能。 **IRow**允许直接访问的单个行对象的列。 如果您事先知道命令执行的结果将生成恰好一个行， **IRow**将检索该行的列。 如果结果集中包括多个行， **IRow**将公开仅第一行。  
  
 **IRow**实现不允许任何导航行。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  **IRow::Open**支持要打开的对象的唯一 DBGUID_STREAM 和 DBGUID_NULL 类型。  
  
 若要获取行对象使用**ICommand::Execute**方法，必须传递 IID_IRow。 **IMultipleResults**必须使用接口来处理多个结果集。 **IMultipleResults**支持**IRow**和**IRowset**。 **IRowset**用于大容量操作。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [使用 IRow 提取 BLOB 数据](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  