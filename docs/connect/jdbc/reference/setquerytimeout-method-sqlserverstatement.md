---
title: setQueryTimeout 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c513265-cd0c-4b38-9494-94458c17a16d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09c984b0d4a0bfa1fedb57f60532a721b16afccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621396"
---
# <a name="setquerytimeout-method-sqlserverstatement"></a>setQueryTimeout 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将驱动程序等待 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象运行的秒数设置为给定的秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setQueryTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parameters  
 *seconds*  
  
 指示要等待秒数的 int，如果没有限制，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setQueryTimeout 方法由 java.sql.Statement 接口中的 setQueryTimeout 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
