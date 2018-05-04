---
title: getLoginTimeout 方法 (SQLServerDataSource) |Microsoft 文档
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
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcaccc8a16561f43b4ada72d1e07bad291b6ec2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>getLoginTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回的秒数此[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象将在尝试建立连接时等待。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>返回值  
 **Int**表示等待的秒数的值。  
  
## <a name="remarks"></a>注释  
 如果应用程序未明确指定超时值，则此方法会返回 15 秒的默认值。  
  
 由 javax.sql.DataSource 接口中的 getLoginTimeout 方法指定此 getLoginTimeout 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
