---
title: execute 方法 (java.lang.String) (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 64ac78b8-d5b3-4134-9b72-d2b0c52168a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b303a9002194f05d1ceb2c3c9f154ed26f6524d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797885"
---
# <a name="execute-method-javalangstring-sqlserverstatement"></a>execute 方法 (java.lang.String) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行可返回多个结果的给定的 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 一个**字符串**，其中包含 SQL 语句。  
  
## <a name="return-value"></a>返回值  
 如果第一个结果为一个结果集，则为“true”。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此执行方法是由 java.sql.Statement 接口中的执行方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [执行方法&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
