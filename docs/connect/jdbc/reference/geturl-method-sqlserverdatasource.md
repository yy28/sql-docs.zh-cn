---
title: getURL 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dd0d5d2c-91fe-4b0f-a162-69d898ba176e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ed41c600f0fc7a82f1f9a4ec3f512e96839191d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910553"
---
# <a name="geturl-method-sqlserverdatasource"></a>getURL 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的 URL。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含 URL 的字符串  。  
  
## <a name="remarks"></a>备注  
 出于安全原因，请不要在提供给 [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) 方法的 URL 中包括密码。 这是因为：第三方 Java 应用程序服务器经常会在其数据源配置用户界面中显示为 URL 属性设置的值。 请改用 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) 方法设置密码值。 Java 应用程序服务器不会在配置用户界面中显示在其数据源中设置的密码。  
  
> [!NOTE]  
>  如果在调用 getURL 方法之前未调用 setURL 方法，则 getURL 将返回默认值“jdbc:sqlserver://”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
