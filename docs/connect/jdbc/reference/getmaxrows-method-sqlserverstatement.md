---
title: getMaxRows 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8cb1c317930d97263038d09bd84e8836d5f6f4ff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773635"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象生成的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象可包含的最大行数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值指示最大行数；如果没有限制，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxRows 方法由 java.sql.Statement 接口中的 getMaxRows 方法指定。  
  
 此 getMaxRows 方法对于动态可滚动游标始终返回 0。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
