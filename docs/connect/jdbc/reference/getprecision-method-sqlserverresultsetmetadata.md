---
title: getPrecision 方法 (SQLServerResultSetMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de46c96e-6ad6-4946-883e-807123658500
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 702686f498526741eba5d216ea629d5463741965
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796057"
---
# <a name="getprecision-method-sqlserverresultsetmetadata"></a>getPrecision 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取指定列的小数位数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPrecision(int column)  
```  
  
#### <a name="parameters"></a>Parameters  
 *column*  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 指示列精度的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getPrecision 方法由 java.sql.ResultSetMetaData 接口中的 getPrecision 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
