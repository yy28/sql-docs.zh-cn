---
title: SQLServerSavepoint 构造函数的保存点 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection, java.lang.StringName.SQLServerSavepoint
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb77db6b-ebf8-4b12-8153-2c4bdb8d72f7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc9da361914b67ab28d37de9b1828ed67850d156
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserversavepoint-constructor-sqlserverconnection-javalangstringname"></a>SQLServerSavepoint 构造函数 (SQLServerConnection, java.lang.StringName)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)类基于给定的连接和名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public SQLServerSavepoint(SQLServerConnection con,  
                          java.lang.String sName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *con*  
  
 A [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。  
  
 *sName*  
  
 A**字符串**包含的保存点的名称。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerSavepoint 构造函数](../../../connect/jdbc/reference/sqlserversavepoint-constructors.md)   
 [SQLServerSavepoint 成员](../../../connect/jdbc/reference/sqlserversavepoint-members.md)   
 [SQLServerSavepoint 类](../../../connect/jdbc/reference/sqlserversavepoint-class.md)  
  
  
