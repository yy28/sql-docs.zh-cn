---
title: getTimestamp 方法 (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (java.lang.String,java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 770668d9-2e52-4ff0-be2f-ebf78fd41644
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 39d50008ac35e592b97ad17726a419c61b2a30e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66767405"
---
# <a name="gettimestamp-method-javalangstring-javautilcalendar"></a>getTimestamp 方法 (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定参数名称，使用 Calendar 对象检索指定参数作为 Java 编程语言中的 java.sql.Timestamp 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String name,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
  
 包含参数名称的字符串  。  
  
 cal   
  
 一个日历对象。  
  
## <a name="return-value"></a>返回值  
 一个时间戳的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTimestamp 方法是由 java.sql.CallableStatement 接口中的 getTimestamp 方法指定的。  
  
 此方法只从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 和 smalldatetime 列返回值   。  
  
## <a name="see-also"></a>另请参阅  
 [getTimestamp 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
