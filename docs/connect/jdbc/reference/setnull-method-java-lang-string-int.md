---
title: setNull 方法 (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d7e267-d9de-407a-b1a9-abdc2623478d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2139a25c4032f4f95b173d4cb5e78fbbc62495f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973534"
---
# <a name="setnull-method-javalangstring-int"></a>setNull 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据要设置的参数的类型，将指定参数设置为 Null 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 nType   
  
 由 java.sql.Types 定义的 JDBC 类型代码。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setNull 方法由 java.sql.CallableStatement 接口中的 setNull 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [setNull 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
