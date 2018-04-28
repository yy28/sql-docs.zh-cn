---
title: setTypeMap 方法 (SQLServerConnection) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerConnection.setTypeMap
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bffd20a6-1310-44b0-9602-974500481fa6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 76085be0b9b393bea09fc4ea6b1839745ec149f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="settypemap-method-sqlserverconnection"></a>setTypeMap 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将给定的 TypeMap 对象的类型映射作为安装此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。  
  
> [!NOTE]  
>  此方法当前不支持通过[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTypeMap(java.util.Map map)  
```  
  
#### <a name="parameters"></a>Parameters  
 *映射*  
  
 一个 TypeMap 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 setTypeMap 方法指定此 setTypeMap 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
