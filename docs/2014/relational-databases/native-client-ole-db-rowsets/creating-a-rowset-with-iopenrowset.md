---
title: 使用 IOpenRowset 创建行集 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7cdce7632aa726d2992a0383d19691569ed57c0a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138190"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>使用 IOpenRowset 创建行集
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持**IOpenRowset::OpenRowset**方法有以下限制：  
  
-   基表或视图必须指定数据库中 ID (DBID) 结构的*pTableID*参数指向。  
  
-   DBID *eKind*成员必须指示 DBKIND_NAME。  
  
-   DBID *uName*成员必须为 Unicode 字符字符串中指定现有的基础表或视图的名称。  
  
-   *PIndexID*参数**OpenRowset**必须为 NULL。  
  
 结果集的**IOpenRowset::OpenRowset**包含单个行集。 可以通过支持包含单个行集的结果集[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标。 游标支持允许开发人员使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并发控制机制。  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  