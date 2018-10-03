---
title: 生成多个行集结果的命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1b1cdefab8f244a7800b66bc85872d752184e22
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852685"
---
# <a name="commands-generating-multiple-rowset-results"></a>生成多个行集结果的命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
  
-   [使用 IMultipleResults 处理多个结果集](../../relational-databases/native-client-ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>请参阅  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
