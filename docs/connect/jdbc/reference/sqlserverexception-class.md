---
title: SQLServerException 类 |Microsoft 文档
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
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56766dec21b0e823174eeccbaf16a02de2b5578a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverexception-class"></a>SQLServerException 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 SQL 语句运行不成功或不完整。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.sql.SQLException  
  
 **实现：** java.io.Serializable  
  
## <a name="syntax"></a>语法  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>注释  
 SQLServerException 类处理 SQL 92 和 XOPEN 状态代码。 可使用用户指定的连接属性在两种代码间切换。 异常将写入已指定的任何打开日志文件。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
