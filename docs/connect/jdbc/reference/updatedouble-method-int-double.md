---
title: updateDouble 方法 (int，double) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDouble (int, double)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90c47643-e27e-425d-85a0-63866f858367
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 243d42ed167c1722cea796215af192213614b22f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746775"
---
# <a name="updatedouble-method-int-double"></a>updateDouble 方法 (int, double)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列索引使用 double 值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateDouble(int index,  
                         double x)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引  
  
 指示列索引的 int。  
  
 *x*  
  
 一个**double**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateDouble 方法由 java.sql.ResultSet 接口中的 updateDouble 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateDouble 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
