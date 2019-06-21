---
title: setClob 方法 （int，java.sql.Clob） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setClob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 68d49f2c-fd8d-4abb-bfdc-e7b0fbd9a9da
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f78d8d226043deed03ab86e5859453313d296fb9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795622"
---
# <a name="setclob-method-int-javasqlclob"></a>setClob 方法 (int, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定 Clob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.sql.Clob clobValue)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterIndex   
  
 指示参数编号的 int  。  
  
 clobValue   
  
 Clob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setClob 方法是由 java.sql.PreparedStatement 接口中的 setClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 方法](../../../connect/jdbc/reference/sqlserverpreparedstatement-methods.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
