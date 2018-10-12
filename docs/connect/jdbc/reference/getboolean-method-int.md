---
title: getBoolean 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBoolean (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d9db847-df22-40ab-8a5c-ec9158c576ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0daf79ac0b27e2f281ff5ef8d0aa86ae284ab4b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667421"
---
# <a name="getboolean-method-int"></a>getBoolean 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引检索指定参数的值作为 boolean 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getBoolean(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个布尔值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBoolean 方法是由 java.sql.CallableStatement 接口中的 getBoolean 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBoolean 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
