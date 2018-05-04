---
title: getURL 方法 (SQLServerDataSource) |Microsoft 文档
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
- SQLServerDataSource.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dd0d5d2c-91fe-4b0f-a162-69d898ba176e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a506fbfd0c35ae57d2d027724b4d671092398de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="geturl-method-sqlserverdatasource"></a>getURL 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的 URL。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**包含的 URL。  
  
## <a name="remarks"></a>注释  
 出于安全原因，你不应包括密码提供给 URL 中[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)方法。 这是因为：第三方 Java 应用程序服务器经常会在其数据源配置用户界面中显示为 URL 属性设置的值。 请改用[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)方法以设置密码值。 Java 应用程序服务器不会在配置用户界面中显示在其数据源中设置的密码。  
  
> [!NOTE]  
>  GetURL setURL 方法未调用调用 getURL 方法之前，如果返回的默认值"jdbc:sqlserver: / /"。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
