---
title: 生成多个行集结果的命令（OLE DB 驱动程序）| Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 如何针对批处理的 SQL 语句返回多个行集以及存储过程何时会实现批处理的 SQL 语句。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- OLE DB Driver for SQL Server, commands
- OLE DB Driver for SQL Server, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93c2d5ec6f5965edc56fea26b8474d3b8926a0cb
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860156"
---
# <a name="commands-generating-multiple-rowset-results"></a>生成多个行集结果的命令
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 可以通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语句返回多个行集。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语句在以下条件下返回具有多个行集的结果：  
  
-   以单个命令的形式提交成批的 SQL 语句。  
  
-   存储过程实现一批 SQL 语句。  
  
## <a name="batches"></a>批处理  
 OLE DB Driver for SQL Server 将分号字符识别为 SQL 语句的批处理分隔符：  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 通过一个批处理发送多个 SQL 语句比单独执行每个 SQL 语句更有效。 发送一个批处理减少了客户端和服务器之间的网络往返。  
  
## <a name="stored-procedures"></a>存储过程  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 为存储过程中的每个语句返回一个结果集，因此大多数 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程返回多个结果集。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 IMultipleResults 处理多个结果集](../../oledb/ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
