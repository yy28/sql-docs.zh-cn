---
title: "getPrecision 方法 (SQLServerResultSetMetaData) |Microsoft 文档"
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
apiname: SQLServerResultSetMetaData.getPrecision
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: de46c96e-6ad6-4946-883e-807123658500
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca52ca740162aee4072e4d389df72b613f765892
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getprecision-method-sqlserverresultsetmetadata"></a>getPrecision 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取指定的列的数目的十进制数字。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPrecision(int column)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列*  
  
 **Int** ，该值指示的列索引。  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示列的精度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSetMetaData 接口中的 getPrecision 方法指定此 getPrecision 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
