---
title: moveToInsertRow 方法 (SQLServerResultSet) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3a53a13c1352f33033a9507b66a4b257265acc3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839732"
---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>moveToInsertRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将游标移到插入行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 moveToInsertRow 方法指定此 moveToInsertRow 方法。  
  
 将游标置于插入行中时，将记住当前游标位置。 插入行是与可更新的结果集关联的特殊行。 它实际上是一个缓冲区，在其中可通过调用 updater 方法来构造新行，之后将该行添加到结果集。  
  
 仅更新程序、 getter 和[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)当光标位于插入行时，可以调用方法。 给定的值每次调用此方法时，并在调用 insertRow 之前，必须是在结果集中的所有列。 对列值调用 getter 之前，必须调用 updater 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
