---
title: getBigDecimal 方法 （java.lang.String，int） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6967ba55-9c9a-4f6f-a4d2-8ee9c9a82c14
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 273321cb3ee41efc498a527ea1693b272108f6eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getbigdecimal-method-javalangstring-int"></a>getBigDecimal 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称和小数位数，检索指定参数的值作为 java.math.BigDecimal。  
  
> [!NOTE]  
>  JDBC 规范已不推荐使用此方法， 相反，应使用[getBigDecimal (java.lang.String)](../../../connect/jdbc/reference/getbigdecimal-method-java-lang-string.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String sCol,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
 *小数位数*  
  
 指示小数点右边的位数的 int。  
  
## <a name="return-value"></a>返回值  
 一个 BigDecimal 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getBigDecimal 方法指定此 getBigDecimal 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getBigDecimal 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
