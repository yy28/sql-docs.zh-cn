---
title: setNull 方法 (java.lang.String, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5137c4df92860822e715d70a1355b490026af40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973556"
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
 sCol   
  
 **字符串**contthat 包含参数名称的 aining。  
  
 nType   
  
 由 java.sql.Types 定义的 JDBC 类型代码。  
  
 sTypeName   
  
 一个指示要设置的参数完全限定名称的 String  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setNull 方法由 java.sql.CallableStatement 接口中的 setNull 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [setNull 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
