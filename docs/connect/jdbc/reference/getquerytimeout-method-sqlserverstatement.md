---
title: getQueryTimeout 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fd4d7b32c9480fec28e20a9dcbc9c22530eb4a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980639"
---
# <a name="getquerytimeout-method-sqlserverstatement"></a>getQueryTimeout 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 等待此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象运行的秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>返回值  
 指示 JDBC 驱动程序将等待秒数的 int  ，如果没有限制，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getQueryTimeout 方法由 getQueryTimeout 方法在 .sql 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
