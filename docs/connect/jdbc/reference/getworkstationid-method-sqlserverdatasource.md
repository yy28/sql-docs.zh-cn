---
title: getWorkstationID 方法 (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 98cde4953d60f13d1768b06dbfab9ada6ea8af55
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978055"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于连接数据源的客户端计算机名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>返回值  
 包含客户端计算机名称的 String  。  
  
## <a name="remarks"></a>备注  
 workstationID 是客户端计算机或工作站的名称。 如果未设置 workstationID 属性，则通过调用 InetAddress.getLocalHost().getHostName() 方法构造默认值。 如果 getHostName 返回空值，则调用 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
