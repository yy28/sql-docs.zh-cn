---
title: close 方法 (SQLServerResultSet) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc2ea42ef473e1d68b12fa20427769e27937ff07
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="close-method-sqlserverresultset"></a>close 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  释放此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象的数据库和 JDBC 资源而等待自动关闭时执行此操作无需立即。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中关闭的方法指定此关闭的方法。  
  
 自动关闭 SQLServerResultSet 对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)它时会生成该 SQLServerStatement 对象已关闭、 重新运行，或用于检索下一个结果的多个结果序列中的对象. 垃圾回收时，还会自动关闭 SQLServerResultSet 对象。  
  
 当执行可生成单个大型只进、只读结果集的语句时，您所感兴趣的可能只是返回的结果集中的一些初始行集。 在这种情况下，应用程序可能调用[取消](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)之前关闭结果相关联的语句对象方法设置以尽量减少放弃所做的剩余的不必要行所需的处理时间。 在决定是否应使用此方法时，建议对照可节约的处理时间与取消执行所需的时间及与服务器之间的附加往返，在两者之间进行折衷。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
