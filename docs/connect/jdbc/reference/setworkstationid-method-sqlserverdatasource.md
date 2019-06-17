---
title: setWorkstationID 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3b9b4dd4ce34dcc39148a2346fd729a8dfb6b87f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773218"
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于连接数据源的客户端计算机名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>Parameters  
 workstationID   
  
 包含客户端计算机名称的 String  。  
  
## <a name="remarks"></a>Remarks  
 workstationID 是客户端计算机或工作站的名称。 如果未设置 workstationID 属性，默认值是通过调用 InetAddress.getLocalHost().getHostName() 方法构造的。 如果 getHostName 返回空白值，称为 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
