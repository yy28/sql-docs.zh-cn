---
title: 使用 IOpenRowset 创建行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7b91b10c2ce266ad648bce0ba1c19946098c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183707"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>使用 IOpenRowset 创建行集
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持**IOpenRowset：： OpenRowset**方法，但有以下限制：  
  
-   必须在 pTableID 参数指向的数据库 ID (DBID) 结构中指定基表或视图**。  
  
-   DBID eKind 成员必须指示 DBKIND_NAME**。  
  
-   DBID uName 成员必须将现有基表或视图的名称指定为 Unicode 字符串**。  
  
-   OpenRowset 的 pIndexID 参数必须为 NULL******。  
  
 IOpenRowset::OpenRowset 的结果集包含单个行集****。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标可以支持[!INCLUDE[msCoName](../../includes/msconame-md.md)]包含单个行集的结果集。 游标支持允许开发人员使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并发控制机制。  
  
## <a name="see-also"></a>另请参阅  
 [行集](rowsets.md)  
  
  
