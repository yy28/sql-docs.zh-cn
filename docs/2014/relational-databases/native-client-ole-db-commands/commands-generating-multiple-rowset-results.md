---
title: 生成多个行集结果的命令 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04a7db670171f6f890f55a89e2da987ef2309f0e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218839"
---
# <a name="commands-generating-multiple-rowset-results"></a>生成多个行集结果的命令
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序可以返回多个行集从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句在以下条件下返回具有多个行集的结果：  
  
-   以单个命令的形式提交成批的 SQL 语句。  
  
-   存储过程实现一批 SQL 语句。  
  
## <a name="batches"></a>批处理  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将分号字符识别为 SQL 语句的批处理分隔符：  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 通过一个批处理发送多个 SQL 语句比单独执行每个 SQL 语句更有效。 发送一个批处理减少了客户端和服务器之间的网络往返。  
  
## <a name="stored-procedures"></a>存储过程  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为存储过程中的每个语句返回一个结果集，因此大多数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程返回多个结果集。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IMultipleResults 处理多个结果集](using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>请参阅  
 [命令](commands.md)  
  
  
