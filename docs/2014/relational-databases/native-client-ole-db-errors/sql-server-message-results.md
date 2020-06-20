---
title: SQL Server 消息结果 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: rothja
ms.author: jroth
ms.openlocfilehash: aa63445b81ec89b87523fa29c50817e128d48515
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043558"
---
# <a name="sql-server-message-results"></a>SQL Server 消息结果
  以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在执行时不会生成 Native Client OLE DB 提供程序行集或受影响的行的计数：  
  
-   PRINT  
  
-   严重性级别为 10 或更低的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 这些语句会返回一个或多个信息性消息，或者使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回信息性消息以替代行集或计数结果。 成功执行时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client OLE DB 提供程序将返回 S_OK，并且消息可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB 提供程序使用者使用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native client OLE DB 提供程序返回 S_OK 并在执行多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或使用者执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序成员函数时提供一条或多条信息性消息。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次执行成员函数后，无论返回代码的值、是否存在返回的 IRowset 或 IMultipleResults 接口引用，或者是否缺少返回的**IRowset**或**IMultipleResults**接口引用或受影响的行的计数，Native Client OLE DB 提供程序使用者允许动态指定查询文本。  
  
## <a name="see-also"></a>另请参阅  
 [错误](errors.md)  
  
  
