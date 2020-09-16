---
description: SQLServerXAConnection 类
title: SQLServerXAConnection 类 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c07c9fdd817ecda1b0f65d936fcba267ed620f26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462549"
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示可参与分布式 (XA) 事务的 JDBC 连接。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **实现：** javax.sql.XAConnection  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>备注  
 SQLServerXAConnection 对象可以通过 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象登记到分布式事务中。 事务管理器通常是中间层服务器的一部分，它通过 SQLServerXAResource 对象管理 SQLServerXAConnection 对象。  
  
> [!NOTE]  
>  应用程序编程人员一般不直接使用此接口。 它主要由在中间层服务器中工作的事务管理器使用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAConnection 成员](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
