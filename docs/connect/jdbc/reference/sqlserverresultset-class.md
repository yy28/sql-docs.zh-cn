---
title: "SQLServerResultSet 类 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac9db37012a51c8ba365b22dd7e56b30ae5b5b6d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverresultset-class"></a>SQLServerResultSet 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 结果集。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **实现：** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>注释  
 结果集有两种类型：客户端与服务器端。  
  
 当结果可容纳于客户端进程内存时，使用客户端结果集。 这些结果提供最快的性能，并由读取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]完全从数据库中。 这些结果集并不会在创建服务器端游标时产生开销而为数据库增加额外负荷。 然而，这些结果集类型不可更新。  
  
 当结果不可容纳于客户端进程内存或当结果集需要调整为可更新时，可使用服务器端结果集。 使用此类型的结果集，JDBC 驱动程序会在用户滚动浏览结果集时，以透明方式创建服务器端游标并提取结果集的行。  
  
 SQLServerResultSet 类提供了很多方法可让你更新结果集与任何本机 Java 数据类型以及许多 Java 对象类型。  
  
 此类支持到 SQLServerResultSet 类、 ISQLServerResultSet 接口和 java.sql.ResultSet 接口解包。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

