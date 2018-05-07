---
title: SQLServerPreparedStatement 类 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c7b37e26faedf7cb064880d68e17f4688bfbe73
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>注释  
 SQLServerPreparedStatement 提供用来提供参数为任何本机 Java 类型和许多的 Java 对象类型的方法。 SQLServerPreparedStatement 准备语句通过使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **sp_prepare**存储的过程，然后重新使用为每个后续的情况下运行的语句，通常使用不同处理的返回的语句用户提供的参数。  
  
 SQLServerPreparedStatement 批处理支持，在其上一组已准备的语句运行单个数据库中往返，以提高运行时性能。  
  
 此类支持到 SQLServerPreparedStatement 类、 ISQLServerPreparedStatement 接口、 java.sql.PreparedStatement 接口的类和接口解包适用于支持 SQLServerStatement 解包。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
