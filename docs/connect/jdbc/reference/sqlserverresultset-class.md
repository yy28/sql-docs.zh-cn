---
title: SQLServerResultSet 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 71513f5e8006adffdb46b249f6358030d11b95a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801504"
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
  
## <a name="remarks"></a>Remarks  
 结果集有两种类型：客户端与服务器端。  
  
 当结果可容纳于客户端进程内存时，使用客户端结果集。 这些结果提供了最快性能，并由 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 从数据库中整个读取。 这些结果集并不会在创建服务器端游标时产生开销而为数据库增加额外负荷。 然而，这些结果集类型不可更新。  
  
 当结果不可容纳于客户端进程内存或当结果集需要调整为可更新时，可使用服务器端结果集。 使用此类型的结果集，JDBC 驱动程序会在用户滚动浏览结果集时，以透明方式创建服务器端游标并提取结果集的行。  
  
 SQLServerResultSet 类提供了很多方法，便于用户使用任何本机 Java 数据类型和很多 Java 对象类型来更新结果集。  
  
 此类支持取消包装 SQLServerResultSet 类、ISQLServerResultSet 接口和 java.sql.ResultSet 接口。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
