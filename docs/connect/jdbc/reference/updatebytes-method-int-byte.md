---
title: updateBytes 方法 （int，字节） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.updateBytes (int, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 625f48ba-53d0-45a6-8fcb-643f1e0cbe8a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0bb2f4de447e2e6bd57581778e321372cf5b651
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updatebytes-method-int-byte"></a>updateBytes 方法 （int，字节）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  会将指定的列更新的数组**字节**给定的列索引的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBytes(int index,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
  
 **Int** ，该值指示的列索引。  
  
 *x*  
  
 数组**字节**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateBytes 方法指定此 updateBytes 方法。  
  
 在以前版本的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，你可以使用 SQLServerResultSet.updateBytes 之间字节数组转换值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型**日期**，**时间**， **datetime2**，或**datetimeoffset**。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [updateBytes 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
