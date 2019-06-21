---
title: setShort 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setShort
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d7031a89-e964-4ffd-87b7-63825799435d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f2bdaf864cba4c95459a2db8f558404c42943d99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782901"
---
# <a name="setshort-method-sqlservercallablestatement"></a>setShort 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 short  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setShort(java.lang.String sCol,  
                     short s)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *s*  
  
 一个**短**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setShort 方法是由 java.sql.CallableStatement 接口中的 setShort 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
