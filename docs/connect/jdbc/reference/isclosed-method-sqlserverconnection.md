---
description: isClosed 方法 (SQLServerConnection)
title: isClosed 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d4a5e3c1d3634e52fd9b2d8244262c40fada06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433589"
---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象是否已关闭。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>返回值  
 如果连接关闭，则为 true****；否则为 false****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isClosed 方法是由 java.sql.Connection 接口中的 isClosed 方法指定的。  
  
 验证调用的 SQLServerConnection 对象的状态。 如果已对连接调用 [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) 方法，或出现一些灾难性错误，则连接关闭。 仅在调用了 close 方法后调用此方法时，它才返回 true****。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
