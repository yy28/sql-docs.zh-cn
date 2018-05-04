---
title: SQLServerCallableStatement 类 |Microsoft 文档
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
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b9942e976f1c6db89cc776f34f7639ff1c8e5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  允许你指定要与输入和输出参数一起使用的要调用的存储过程名称。 此类还可以使用 ?  = call( ?, ..) 语法检索返回状态值。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **实现：** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **扩展：** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>注释  
 SQLServerCallableStatement 允许您指定要调用以及输入和输出参数的存储的过程名称。 SQLServerCallableStatement 还提供的功能，若要检索的返回状态值与`? = call( ?, ..)`语法。  
  
 此类支持到 SQLServerCallableStatement 类、 ISQLServerCallableStatement 接口、 java.sql.CallableStatement 接口的类和接口解包适用于支持 SQLServerPreparedStatement 解包。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 如果该类型与使用指定的类型冲突时 SQLServerCallableStatement 之一设置方法调用对于类型， [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)，使用指定的最后一个 SQLServerCallableStatement set 方法的类型。 但是这可能导致出现不兼容的数据类型转换错误。 如果 SQLServerCallableStatement set 方法未调用，第一个指定的类型[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)调用使用。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 符合的结果集的 JDBC 4.0 建议，以及检索输出参数之前必须检索到更新计数。 如果在完全处理该结果集和更新计数前检索 OUT 参数，则将丢失尚未处理的结果集和更新计数。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
