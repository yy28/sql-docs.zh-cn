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
manager: craigg
ms.openlocfilehash: 27ee52e2dd8acb976d732baa76d32a0401ba445d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666085"
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
  
 包含参数名称的字符串。  
  
 *cal*  
  
 一个日历对象。  
  
## <a name="return-value"></a>返回值  
 一个时间戳的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTimestamp 方法由 java.sql.CallableStatement 接口中的 getTimestamp 方法指定。  
  
 此方法只从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 和 smalldatetime 列返回值。  
  
## <a name="see-also"></a>另请参阅  
 [getTimestamp 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
