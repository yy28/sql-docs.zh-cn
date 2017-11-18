---
title: "getResponseBuffering 方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7d17eb34ef5acdeea9870d1b330423c015bf23a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此缓冲模式响应[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**包含小写**完整**或**自适应**。  
  
## <a name="remarks"></a>注释  
 **自适应**指定缓冲最小可能的数据在必要时。  
  
 **完整**指定在运行时从服务器读取整个结果。  
  
 **自适应**是 JDBC 驱动程序版本 2.0 和 3.0 中的默认值。 **完整**JDBC 驱动程序版本 2.0 之前默认值是。  
  
 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setResponseBuffering 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

