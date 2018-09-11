---
title: SQLServerConnection 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4746e09839e2015e4b7b14963ae698c66066ac78
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784519"
---
# <a name="sqlserverconnection-class"></a>SQLServerConnection 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示连接至 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的 JDBC 连接。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **实现：** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)、java.io.Serializable  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerConnection 支持 JDBC 连接池，并且可以是物理 JDBC 连接或逻辑 JDBC 连接。 SQLServerConnection 可管理通过它创建的所有语句的事务控制，并且可参与通过 XAResource 适配器管理的 XA 分布式事务。  
  
 SQLServerConnection 管理已准备的语句句柄的池。 预定义语句仅准备一次，但通常使用不同的语句参数数据值运行多次。 预定义语句还可跨多个关闭的逻辑（入池）连接进行维护。  
  
> [!NOTE]  
>  SQLServerConnection 不是线程安全。 但是，可以在并发线程中同时处理基于单个连接创建的多个语句。  
  
 此类支持取消对 SQLServerConnection 类、 按 java.sql.connection 接口和 ISQLServerConnection 接口。 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
