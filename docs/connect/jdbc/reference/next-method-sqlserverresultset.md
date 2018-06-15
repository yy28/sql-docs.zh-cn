---
title: 下一步方法 (SQLServerResultSet) |Microsoft 文档
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
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa878b809af8dab927877f8af0db3d54a6a3eb30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32840822"
---
# <a name="next-method-sqlserverresultset"></a>下一步方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将游标从当前位置下移一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>返回值  
 **true**新的当前行是否有效。 **false**如果没有更多的行来处理。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 此下一个方法被指定 java.sql.ResultSet 接口中的下一步方法。  
  
 结果集游标最初位于第一行之前。 对下一步的方法的第一个调用将第一行作为当前行，第二个调用作出第二个行的当前行中，依次类推。  
  
 如果打开当前行的输入的流，对下一步的方法的调用将隐式关闭它。 警告链[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)时读取新行时，对象将被清除。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
