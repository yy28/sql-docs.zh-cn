---
title: "setNull 方法 （java.lang.String、 int、 java.lang.String） |Microsoft 文档"
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
- SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56bf1d05bc51ebfc9b18e7dd7ba92942ce777638
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setnull-method-javalangstring-int-javalangstring"></a>setNull 方法 (java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据要设置的参数的类型和名称，将指定参数设置为 Null 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType,  
                    java.lang.String sTypeName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 A**字符串**contthat 包含 aining 参数名称。  
  
 *nType*  
  
 由 java.sql.Types 定义的 JDBC 类型代码。  
  
 *sTypeName*  
  
 A**字符串**，该值指示在设置参数的完全限定的名称。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 setNull 方法指定此 setNull 方法。  
  
## <a name="see-also"></a>另请参阅  
 [setNull 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
