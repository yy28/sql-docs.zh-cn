---
title: SQLServerPreparedStatement 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7112a20f7811a0796396045c50b1b243ed0c3802
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796947"
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 预定义语句功能的基本实现。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** SQLServerStatement  
  
 **实现：** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerPreparedStatement 可提供使你能够提供作为任意本机 Java 类型和许多 Java 对象类型的参数的方法。 SQLServerPreparedStatement 通过使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sp_prepare 存储过程来定义某个语句，然后通常使用用户提供的不同参数对每个后续运行的语句重用返回的语句句柄  。  
  
 SQLServerPreparedStatement 支持通过批处理（即在单个数据库往返通信中运行一组预定义语句）来改善运行时性能。  
  
 此类支持取消对 SQLServerPreparedStatement 类、 ISQLServerPreparedStatement 接口、 java.sql.PreparedStatement 接口的类和接口支持的 SQLServerStatement 解包。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
