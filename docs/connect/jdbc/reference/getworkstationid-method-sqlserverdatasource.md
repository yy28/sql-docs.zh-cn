---
title: getWorkstationID 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ece266f25a57c2a99e8acb0b308f7bd918189057
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673625"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的客户端计算机名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>返回值  
 包含客户端计算机名称的 String。  
  
## <a name="remarks"></a>Remarks  
 workstationID 是客户端计算机或工作站的名称。 如果未设置 workstationID 属性，默认值是通过调用 InetAddress.getLocalHost().getHostName() 方法构造的。 如果 getHostName 返回空白值，称为 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
