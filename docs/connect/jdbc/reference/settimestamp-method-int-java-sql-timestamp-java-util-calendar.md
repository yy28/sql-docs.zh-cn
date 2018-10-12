---
title: setTimestamp 方法 (int, java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTimestamp (int, java.sql.Timestamp, java.util.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10c93cbf-f831-4e00-8e37-ea728bf34b1e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c1cfbda2b7ac6530242cfb4ff6191fd733865d8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712205"
---
# <a name="settimestamp-method-int-javasqltimestamp-javautilcalendar"></a>setTimestamp 方法 (int, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的时间戳和日历值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setTimestamp(int n,  
                               java.sql.Timestamp x,  
                               java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 *n*  
  
 指示参数编号的 int。  
  
 *x*  
  
 一个时间戳的对象。  
  
 *cal*  
  
 一个日历对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setTimestamp 方法是由 java.sql.PreparedStatement 接口中的 setTimestamp 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setTimestamp 方法 (SQLServerPreparedStatement)](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
