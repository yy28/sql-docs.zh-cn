---
title: close 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec9b51d08e10df0f829308d163b573c0670c78e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637255"
---
# <a name="close-method-sqlserverresultset"></a>close 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  立即释放此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的数据库和 JDBC 资源，而不是在此对象自动关闭时等待上述操作发生。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 close 方法是由 java.sql.ResultSet 接口中的 close 方法指定的。  
  
 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象会自动关闭其在 SQLServerStatement 对象关闭、重新运行或用于从一个多结果序列中检索下一个结果时生成的 SQLServerResultSet 对象。 对 SQLServerResultSet 对象进行垃圾收集处理后，此对象会自动关闭。  
  
 当执行可生成单个大型只进、只读结果集的语句时，您所感兴趣的可能只是返回的结果集中的一些初始行集。 在此情况下，应用程序可能会在关闭结果集之前调用关联语句对象的 [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 方法，以最大程度地减少放弃余下不必要的行所需要的处理时间。 在决定是否应使用此方法时，建议对照可节约的处理时间与取消执行所需的时间及与服务器之间的附加往返，在两者之间进行折衷。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
