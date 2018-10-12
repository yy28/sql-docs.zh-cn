---
title: getClob 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ad871d09-ec43-4885-9067-20854b439b0c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f546a846b96b3c0d518663fbf52edb033631a7ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647615"
---
# <a name="getclob-method-javalangstring"></a>getClob 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定 JDBC BLOB 参数作为 Java 编程语言中的 Clob 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Clob getClob(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
## <a name="return-value"></a>返回值  
 Clob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getClob 方法是由 java.sql.CallableStatement 接口中的 getClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
