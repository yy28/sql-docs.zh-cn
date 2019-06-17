---
title: moveToInsertRow 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c841052f4fad09905f0aab447af9441919a23f1c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779570"
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
  
## <a name="remarks"></a>Remarks  
 此 moveToInsertRow 方法由 java.sql.ResultSet 接口中的 moveToInsertRow 方法指定。  
  
 将游标置于插入行中时，将记住当前游标位置。 插入行是与可更新的结果集关联的特殊行。 它实际上是一个缓冲区，在其中可通过调用 updater 方法来构造新行，之后将该行添加到结果集。  
  
 当游标位于插入行上时，只能调用 updater、getter 和 [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 方法。 每次调用此方法且在调用 insertRow 之前，都必须为结果集中的所有列指定值。 对列值调用 getter 之前，必须调用 updater 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
