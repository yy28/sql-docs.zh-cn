---
description: setTrustManagerClass 方法 (SQLServerDataSource)
title: setTrustManagerClass 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setTrustManagerClass
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 74a82516e982e9bf84d00939cb93bc5f9eda502e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354953"
---
# <a name="settrustmanagerclass-method-sqlserverdatasource"></a>setTrustManagerClass 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置 TrustManagerClass 连接属性的 String 值。
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTrustManagerClass(java.lang.String trustManagerClass)  
```  
  
#### <a name="parameters"></a>参数  
 *trustManagerClass*  
  
 String****，它包含自定义 javax.net.ssl.TrustManager 的完全限定类名。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
