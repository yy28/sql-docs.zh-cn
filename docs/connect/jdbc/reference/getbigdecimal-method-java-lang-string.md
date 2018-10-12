---
title: getBigDecimal 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d0b29b48-9663-4de4-9fc2-82bc30e44aed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff651f2cc52ebca4b6d10a4e9cb01eebbb736970
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734515"
---
# <a name="getbigdecimal-method-javalangstring"></a>getBigDecimal 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定参数具有全精度的 java.math.BigDecimal 的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的 String。  
  
## <a name="return-value"></a>返回值  
 一个 BigDecimal 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBigDecimal 方法由 java.sql.CallableStatement 接口中的 getBigDecimal 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [getBigDecimal 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
