---
title: "getMoreResults 方法 （) |Microsoft 文档"
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
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8259b562590d21c57f0780260f50bf15032a7ead
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getmoreresults-method-"></a>getMoreResults 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将移动到下一个结果此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果返回的结果是一个结果集。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 getMoreResults 方法指定此 getMoreResults 方法。  
  
 隐式调用 getMoreResults 方法关闭所获得的采用任何当前打开的结果集对象[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)方法。  
  
## <a name="see-also"></a>另请参阅  
 [getMoreResults 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
