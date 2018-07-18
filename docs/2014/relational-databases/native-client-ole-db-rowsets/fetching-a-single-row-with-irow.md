---
title: 提取使用 IRow 单行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 243d57b5e42e2c4ecebec6ce1e05d3061baa0a2c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412396"
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 提取单行
  **IRow**接口中的实现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序简化，以提高性能。 **IRow**允许直接访问单行对象的列。 如果您预先知道命令执行的结果将生成一个行**IRow**将检索该行的列。 如果结果集包含多个行**IRow**将公开仅将第一行。  
  
 **IRow**实现不允许的行的任何导航。 行中的每一列只能访问一次，以下情况例外：可以访问一次列以查找列大小，再次访问以提取数据。  
  
> [!NOTE]  
>  **Irow:: Open**支持要打开的对象的唯一 DBGUID_STREAM 和 DBGUID_NULL 类型。  
  
 若要获取行对象使用**icommand:: Execute**方法，必须传递 IID_IRow。 **IMultipleResults**必须使用接口来处理多个结果集。 **IMultipleResults**支持**IRow**并**IRowset**。 **IRowset**用于大容量操作。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [使用 IRow 提取 BLOB 数据](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  
