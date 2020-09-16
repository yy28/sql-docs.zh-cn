---
description: getCatalog 方法 (SQLServerConnection)
title: getCatalog 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc4b720ccf920d1f9fe97ed29f2a2a237e24939e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436879"
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象的当前目录名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含目录名称的字符串  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getCatalog 方法是由 java.sql.Connection 接口中的 getCatalog 方法指定的。  
  
 返回 SQLServerConnection 对象的当前目录属性；如果未设置，则返回 Null。 使用 [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) 方法显式设置目录属性，或者可通过读取当前目录的 TDS 环境更改隐式更新目录属性。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
