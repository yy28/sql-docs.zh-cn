---
title: "SQLServerClob 构造函数 （SQLServerConnection，java.lang.String） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 028d7d4803ff53f518067d869fa192512209d723
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob 构造函数 (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)类在给定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象和数据的字符串。  
  
> [!NOTE]  
>  JDBC 驱动程序 2.0 版已不推荐使用此方法， 请改用[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
## <a name="syntax"></a>语法  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>Parameters  
 *连接*  
  
 一个 SQLServerConnection 对象。  
  
 *数据*  
  
 CLOB 数据。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 构造函数](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

