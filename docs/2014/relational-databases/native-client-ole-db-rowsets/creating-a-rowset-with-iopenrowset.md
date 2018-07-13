---
title: 使用 IOpenRowset 创建行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30ba5a4d1cbe326be567a3be18cd7a76371f7e49
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417936"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>使用 IOpenRowset 创建行集
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持**iopenrowset:: Openrowset**方法有以下限制：  
  
-   基表或视图必须指定在数据库中 ID (DBID) 结构*pTableID*参数指向。  
  
-   DBID *eKind*成员必须指示 DBKIND_NAME。  
  
-   DBID *uName*成员必须为 Unicode 字符字符串指定现有的基础表或视图的名称。  
  
-   *PIndexID*的参数**OpenRowset**必须为 NULL。  
  
 结果集**iopenrowset:: Openrowset**包含单个行集。 可以通过支持结果集包含单个行集[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标。 游标支持允许开发人员使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并发控制机制。  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  
