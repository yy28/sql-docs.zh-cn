---
title: setInt 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setInt
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7de05cf4-3a48-4c60-9a1b-6ad2ae43d258
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 89741f02e9a2afa7c1dc8de6f76f599c70a5a45a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779854"
---
# <a name="setint-method-sqlservercallablestatement"></a>setInt 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 int  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setInt(java.lang.String sCol,  
                   int i)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *i*  
  
 **Int**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setInt 方法是由 java.sql.CallableStatement 接口中的 setInt 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
