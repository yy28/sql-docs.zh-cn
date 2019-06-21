---
title: setLong 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setLong
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 137416fe-a580-424e-be79-fe946eba9e6e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e10e06460ee04abeace42af47c84270901fa1a17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799239"
---
# <a name="setlong-method-sqlservercallablestatement"></a>setLong 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 long  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLong(java.lang.String sCol,  
                    long l)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *l*  
  
 一个**长**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setLong 方法是由 java.sql.CallableStatement 接口中的 setLong 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
