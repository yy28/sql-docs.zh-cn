---
title: setURL 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29e1b67caaf566f04cf01c7c93a5e8d2445c31ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633945"
---
# <a name="seturl-method-sqlserverdatasource"></a>setURL 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于连接数据源的 URL。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parameters  
 *url*  
  
 一个包含 URL 的 String。  
  
## <a name="remarks"></a>Remarks  
 出于安全原因，请不要在提供给 setURL 方法的 URL 中包括密码。 这是因为：第三方 Java 应用程序服务器经常会在其数据源配置用户界面中显示为 URL 属性设置的值。 请改用 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) 方法设置密码值。 Java 应用程序服务器不会在配置用户界面中显示在其数据源中设置的密码。  
  
> [!NOTE]  
>  如果在调用 [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) 方法之前未调用 setURL 方法，则 getURL 将返回默认值“jdbc:sqlserver://”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
