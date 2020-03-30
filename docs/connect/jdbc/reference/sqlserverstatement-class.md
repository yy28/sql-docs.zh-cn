---
title: SQLServerStatement 类 | Microsoft Docs
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
ms.openlocfilehash: 89547655fd734ca9e6e340d94832dea5816f2733
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970376"
---
# <a name="sqlserverstatement-class"></a>SQLServerStatement 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 语句功能的基本实现。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **实现：** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>备注  
 SQLServerStatement 类还提供了大量基类实现方法，以用于 JDBC 准备就绪语句和可调用语句。 SQLServerStatement 类的基本作用是先运行 SQL 语句，再向用户应用程序返回更新计数和结果集。  
  
 此类支持取消包装 SQLServerStatement 类、ISQLServerStatement 接口和 java.sql.Statement 接口。 有关详细信息，请参阅[包装器和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
