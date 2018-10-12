---
title: SQLServerStatement 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7488efcb3392623e6f54cff440a16494c10e0a69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705345"
---
# <a name="sqlserverstatement-class"></a>SQLServerStatement 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 语句功能的基本实现。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **实现：**[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerStatement 类还提供了大量基类实现方法，以用于 JDBC 准备就绪语句和可调用语句。 SQLServerStatement 类的基本作用是先运行 SQL 语句，再向用户应用程序返回更新计数和结果集。  
  
 此类支持取消对 SQLServerStatement 类、ISQLServerStatement 接口和 java.sql.Statement 接口。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
