---
title: executeUpdate 方法 （) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a4d3caaa9cad0b1e9c47edece18015e6d270f1b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-"></a>executeUpdate 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在此运行的 SQL 语句[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)对象，它必须是 SQL INSERT、 UPDATE、 MERGE 或 DELETE 语句; 或返回任何内容，例如 DDL 语句的 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>返回值  
 一个指示受影响的行数的 int，如果使用 DDL 语句，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 executeUpdate 方法指定此 executeUpdate 方法。  
  
## <a name="see-also"></a>另请参阅  
 [executeUpdate 方法&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
