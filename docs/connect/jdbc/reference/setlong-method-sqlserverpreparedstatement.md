---
title: setLong 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setLong
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 08223a62-6489-44e4-85e8-b45bfbb11cfc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d0c1383ddbd9f86089095e90a218f991a4591b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804895"
---
# <a name="setlong-method-sqlserverpreparedstatement"></a>setLong 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 long 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setLong(int n,  
                          long x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *n*  
  
 指示参数编号的 int。  
  
 *x*  
  
 一个**长**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setLong 方法是由 java.sql.PreparedStatement 接口中的 setLong 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
