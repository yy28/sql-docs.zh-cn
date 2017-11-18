---
title: "getUser 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9de58a65490961002fbdcfa37d0a2367ca078382
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getuser-method-sqlserverdatasource"></a>getUser 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**包含的用户名称。  
  
## <a name="remarks"></a>注释  
 [SetUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)方法设置连接到的实例时将使用的用户名[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 如果未设置用户名值，则 getUser 方法返回默认值 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

