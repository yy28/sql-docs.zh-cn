---
title: getUser 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aee686bd06ce449f3dc42c1e7206228e93e66d96
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782372"
---
# <a name="getuser-method-sqlserverdatasource"></a>getUser 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含用户名的字符串  。  
  
## <a name="remarks"></a>Remarks  
 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 方法设置在连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例时将使用的用户名。 如果未设置用户名值，则 getUser 方法返回默认值 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
