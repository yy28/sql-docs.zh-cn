---
title: "setArray 方法 (SQLServerPreparedStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerPreparedStatement.setArray
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b7fb66d4-6a42-43d0-ba68-8514816917cb
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10db7f1cd7f9925275b3ad9ab104263aaeb5b4a3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="setarray-method-sqlserverpreparedstatement"></a>setArray 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数号设置为给定的数组对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setArray(int i,  
                           java.sql.Array x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *我*  
  
 **Int** ，该值指示参数号。  
  
 *x*  
  
 一个数组对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 setArray 方法指定此 setArray 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
