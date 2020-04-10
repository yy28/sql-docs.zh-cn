---
title: getMaxRows 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fe813f8714bf9171873731cee68ac228dd3ace2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906863"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象生成的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象可包含的最大行数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值指示最大行数；如果没有限制，则为 0  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getMaxRows 方法是由 java.sql.Statement 接口中的 getMaxRows 方法指定的。  
  
 此 getMaxRows 方法对于动态可滚动游标始终返回 0。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
