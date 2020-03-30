---
title: 设置时间戳和日历值的 setTimestamp 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp, java.util.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 09dca1f9-225a-4acb-9857-9a947e0829be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58489b749e58981ea385842528b8eac0bca43780
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972391"
---
# <a name="settimestamp-method-javalangstring-javasqltimestamp-javautilcalendar"></a>setTimestamp 方法 (java.lang.String, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的时间戳和日历值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp x,  
                         java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *x*  
  
 Timestamp 对象。  
  
 *c*  
  
 Calendar 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setTimestamp 方法是由 java.sql.CallableStatement 接口中的 setTimestamp 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setTimestamp 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
