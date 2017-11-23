---
title: "setDate 方法为日期和日历-字符串 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.setDate (java.lang.String, java.sql.Date, java.util.Calendar)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: fd152ad6-dd5e-49ef-b166-917371a2cba6
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81250aa6d8b45807b4fc01f8e370ff2e9b911c31
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="setdate-method-javalangstring-javasqldate-javautilcalendar"></a>setDate 方法 (java.lang.String, java.sql.Date, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的日期和日历值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setDate(java.lang.String sCol,  
                    java.sql.Date x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>Parameters  
 *n*  
  
 **Int** ，该值指示参数号。  
  
 *x*  
  
 Date 对象。  
  
 *c*  
  
 日历对象中。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 SetDate 方法 java.sql.CallableStatement 界面中指定此 setDate 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
