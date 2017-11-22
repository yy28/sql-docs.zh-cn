---
title: "setURL 方法 (SQLServerDataSource) |Microsoft 文档"
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
apiname: SQLServerDataSource.setURL
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 222948f40537e84e0c294f05fd8d953b61f53f65
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="seturl-method-sqlserverdatasource"></a>setURL 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于连接到数据源的 URL。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parameters  
 *url*  
  
 A**字符串**包含的 URL。  
  
## <a name="remarks"></a>注释  
 出于安全原因，不应在提供给 setURL 方法的 URL 中包括密码。 这是因为：第三方 Java 应用程序服务器经常会在其数据源配置用户界面中显示为 URL 属性设置的值。 请改用[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)方法以设置密码值。 Java 应用程序服务器不会在配置用户界面中显示在其数据源中设置的密码。  
  
> [!NOTE]  
>  如果 setURL 方法未调用，然后再调[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)方法，getURL 返回的默认值"jdbc:sqlserver: / /"。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
