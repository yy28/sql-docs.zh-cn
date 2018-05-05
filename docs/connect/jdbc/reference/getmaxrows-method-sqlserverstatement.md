---
title: getMaxRows 方法 (SQLServerStatement) |Microsoft 文档
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
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d619f9505d9f6f5e9c2c6db7751ecb224fa2f5e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索最大行数， [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)由此产生的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象可以包含。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示最大行数或 0，如果没有任何限制。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 getMaxRows 方法指定此 getMaxRows 方法。  
  
 此 getMaxRows 方法始终返回 0 为动态的可滚动游标。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
