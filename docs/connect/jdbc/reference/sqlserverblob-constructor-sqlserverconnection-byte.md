---
title: "SQLServerBlob 构造函数 （SQLServerConnection，字节） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnection, byte[].SQLServerBlob
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b75ad63c8bbf1a928c8a464b3997713f4a6e582e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob 构造函数 （SQLServerConnection，字节）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)类在给定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象和一个**字节**数组。  
  
> [!NOTE]  
>  JDBC 驱动程序 2.0 版已不推荐使用此方法， 请改用[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
## <a name="syntax"></a>语法  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parameters  
 *连接*  
  
 一个 SQLServerConnection 对象。  
  
 *数据*  
  
 A**字节**数组。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 构造函数](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
