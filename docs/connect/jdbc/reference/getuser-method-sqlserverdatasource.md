---
description: getUser 方法 (SQLServerDataSource)
title: getUser 方法 (SQLServerDataSource) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b3f1cf26d395e982c21f7f4819ff19b4e633719
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433849"
---
# <a name="getuser-method-sqlserverdatasource"></a>getUser 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含用户名的字符串****。  
  
## <a name="remarks"></a>注解  
 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 方法设置在连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例时将使用的用户名。 如果未设置用户名值，则 getUser 方法返回默认值 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
