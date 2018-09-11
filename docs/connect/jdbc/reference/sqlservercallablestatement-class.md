---
title: SQLServerCallableStatement 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dca164af73506119cfaef376bcb7776708f76df
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785272"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  允许你指定要与输入和输出参数一起使用的要调用的存储过程名称。 此类还可以使用 ?  = call( ?, ..) 语法检索返回状态值。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **实现：**[ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **扩展：**[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerCallableStatement 使你能够指定要与输入和输出参数一起调用的存储过程名称。 SQLServerCallableStatement 还提供的功能来检索返回状态值与`? = call( ?, ..)`语法。  
  
 此类支持取消对 SQLServerCallableStatement 类、 ISQLServerCallableStatement 接口、 java.sql.CallableStatement 接口的类和 SQLServerPreparedStatement 解包支持的接口。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 设置方法 SQLServerCallableStatement 之一对于类型，如果调用的类型与使用指定的类型冲突[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)，使用指定的最后一个 SQLServerCallableStatement set 方法的类型。 但是这可能导致出现不兼容的数据类型转换错误。 如果未调用 SQLServerCallableStatement set 方法，则将使用第一个 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 调用所指定的类型。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 符合 JDBC 4.0 建议，即在检索 OUT 参数之前必须检索一个结果集和更新计数。 如果在完全处理该结果集和更新计数前检索 OUT 参数，则将丢失尚未处理的结果集和更新计数。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
