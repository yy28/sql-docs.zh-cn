---
title: "getNString 方法 (int) (SQLServerResultSet) |Microsoft 文档"
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
ms.assetid: c8cc4636-01e9-4dc8-a40c-728337ca08f5
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd72b796ee87e21b1c480af87c5510e8de83e722
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getnstring-method-int-sqlserverresultset"></a>getNString 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为一个字符串对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getNString(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
## <a name="return-value"></a>返回值  
 一个字符串对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.SQLServerResultSet 接口中的 getNString 方法指定此 getNString 方法。  
  
 此方法可以用于检索的值**nvarchar**， **nchar**， **nvarchar (max)**， **ntext**，或**xml**此当前行中的列[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。 如果尝试使用此方法检索其他数据类型的值，则会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNString 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
