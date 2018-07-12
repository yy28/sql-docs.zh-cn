---
title: SQL Server 消息结果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5db120da45f57debacd2717983fe4ea4118cabe
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431836"
---
# <a name="sql-server-message-results"></a>SQL Server 消息结果
  以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句不会生成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口行集或计数受影响的行时执行：  
  
-   PRINT  
  
-   严重性级别为 10 或更低的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 这些语句会返回一个或多个信息性消息，或者使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回信息性消息以替代行集或计数结果。 在成功执行时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口返回 S_OK，并且消息可供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口使用者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口返回 S_OK，并具有一个或多个信息性消息之后执行多个[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或使用者执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口成员函数。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口使用者允许动态指定查询文本应不考虑的值的返回代码、 是否存在返回每个成员函数执行后检查错误接口**IRowset**或**IMultipleResults**接口引用或受影响的行的计数。  
  
## <a name="see-also"></a>请参阅  
 [错误](errors.md)  
  
  
