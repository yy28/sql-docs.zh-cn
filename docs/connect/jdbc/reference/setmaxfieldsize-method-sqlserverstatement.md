---
title: setMaxFieldSize 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38f7fc1d-acad-4d10-9fc8-3c0669d93b07
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8662d9e3143f61fae03c7158494015f42f4838bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672555"
---
# <a name="setmaxfieldsize-method-sqlserverstatement"></a>setMaxFieldSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将存储字符或二进制值的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 列中的最大字节数限制设置为给定的字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setMaxFieldSize(int max)  
```  
  
#### <a name="parameters"></a>Parameters  
 max  
  
 指示最大字节数的 int 值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setMaxFieldSize 方法由 java.sql.Statement 接口中的 setMaxFieldSize 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
