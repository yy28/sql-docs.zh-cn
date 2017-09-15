---
title: "setPoolable 方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 674f138128dcfda2dc4b924e3b04f148d42b69c5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  请求语句入池或不入池。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>Parameters  
 *能合并*  
  
 如果**true**，请求该语句可存入池中。 如果**false**，请求不合并该语句。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 中指定的值*能合并*参数是对，该值指示应用程序是否想要放入池中的语句的语句池实现的提示。 语句池管理器决定应用程序是否使用该提示。  
  
 语句的池值既应用于由驱动程序实现的内部语句缓存，也应用于由应用程序服务器和其他应用程序实现的外部语句缓存。  
  
 默认情况下，不能合并时创建 SQLServerStatement 对象。 SQLServerPreparedStatement 和 SQLServerCallableStatement 对象是在创建时能合并。  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)如果在已关闭的语句上调用此方法引发。  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)返回一个值，该值指示对象是否能合并。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
