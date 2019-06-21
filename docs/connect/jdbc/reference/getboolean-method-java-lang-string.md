---
title: getBoolean 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBoolean (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c9ee851f-1827-42f5-a50a-bdef3e323a5e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 55174bc7e7a5b91910a9f76239cd0ed85ee78548
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771602"
---
# <a name="getboolean-method-javalangstring"></a>getBoolean 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称检索指定参数作为 boolean 值  的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getBoolean(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个布尔值  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBoolean 方法是由 java.sql.CallableStatement 接口中的 getBoolean 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBoolean 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
