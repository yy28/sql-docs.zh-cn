---
title: SQLServerResultSet 类 | Microsoft Docs
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
ms.openlocfilehash: 7e0a2185037f54aa7ed975667c0bdd5fb921c845
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970611"
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
  
## <a name="remarks"></a>备注  
 结果集有两种类型：客户端与服务器端。  
  
 当结果可容纳于客户端进程内存时，使用客户端结果集。 这些结果提供了最快性能，并由 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 从数据库中整个读取。 这些结果集并不会在创建服务器端游标时产生开销而为数据库增加额外负荷。 然而，这些结果集类型不可更新。  
  
 当结果不可容纳于客户端进程内存或当结果集需要调整为可更新时，可使用服务器端结果集。 使用此类型的结果集，JDBC 驱动程序会在用户滚动浏览结果集时，以透明方式创建服务器端游标并提取结果集的行。  
  
 SQLServerResultSet 类提供了很多方法，便于用户使用任何本机 Java 数据类型和很多 Java 对象类型来更新结果集。  
  
 此类支持取消包装 SQLServerResultSet 类、ISQLServerResultSet 接口和 java.sql.ResultSet 接口。 有关详细信息，请参阅[包装器和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
