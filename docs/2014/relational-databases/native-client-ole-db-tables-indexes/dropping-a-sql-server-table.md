---
title: 删除 SQL Server 表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6f005b9ab1c3d334242b2a20d47f6e4646d6cef8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704539"
---
# <a name="dropping-a-sql-server-table"></a>删除 SQL Server 表
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序公开**ITableDefinition：:D roptable**函数。 这允许使用者 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 从数据库中删除表。  
  
 在 pTableID 参数的 uName 联合的 pwszName 成员中，使用者将表名指定为 Unicode 字符串******。 pTableID 的 eKind 成员必须是 DBKIND_NAME   。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](tables-and-indexes.md)  
  
  
