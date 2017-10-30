---
title: "moveToCurrentRow 方法 (SQLServerResultSet) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.moveToCurrentRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9a7c754c-2d72-4207-b3bd-2afc6047fb3d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8548c196214955e03a04a9a318a30701b0b26f1e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# moveToCurrentRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  把游标移动到记住的游标位置，通常为当前行。  
  
## 语法  
  
```  
  
public void moveToCurrentRow()  
```  
  
## 异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## 注释  
 由 java.sql.ResultSet 接口中的 moveToCurrentRow 方法指定此 moveToCurrentRow 方法。  
  
 如果游标未处在插入行中，此方法没有作用。  
  
## 另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

