---
title: setBigDecimal 方法 (SQLServerPreparedStatement) |Microsoft 文档
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
- SQLServerPreparedStatement.setBigDecimal
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 860f86db-d840-401a-a5c2-cd22e8cc1e4e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24de604f922f879d55920e9d6cd3086c79078185
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setbigdecimal-method-sqlserverpreparedstatement"></a>setBigDecimal 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数号设置为给定的 BigDecimal 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setBigDecimal(int n,  
                                java.math.BigDecimal x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *n*  
  
 **Int** ，该值指示参数号。  
  
 *x*  
  
 一个 BigDecimal 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 setBigDecimal 方法指定此 setBigDecimal 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
