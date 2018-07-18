---
title: getUser 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cd095dc3968ae89dfedb110cc5a75eb1b19844a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839232"
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
  
  
