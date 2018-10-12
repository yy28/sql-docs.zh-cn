---
title: SQLServerException 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfcc73705d04b3d3efa7515f74676b0eda120323
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680275"
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
  
## <a name="remarks"></a>Remarks  
 SQLServerException 类可处理 SQL 92 和 XOPEN 状态代码。 可使用用户指定的连接属性在两种代码间切换。 异常将写入已指定的任何打开日志文件。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
