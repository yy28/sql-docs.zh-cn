---
title: getURL 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb709f6b-64e1-4d0c-a704-290891627dd7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: add077cc98e9453b5523c816ff9c47b67a13272c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779816"
---
# <a name="geturl-method-javalangstring"></a>getURL 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定参数作为 Java 编程语言中的 URL 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.net.URL getURL(java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parameters  
 *s*  
  
 包含参数名称的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个 URL 的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getURL 方法是由 java.sql.CallableStatement 接口中的 getURL 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getURL 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
