---
title: getColumnLabel 方法 (SQLServerResultSetMetaData) |Microsoft 文档
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
- SQLServerResultSetMetaData.getColumnLabel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cf67692c-24aa-49e6-8e88-a47d4e8c021c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6fc4940874ab44caccdfb9df60c6584b0cc50884
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32831792"
---
# <a name="getcolumnlabel-method-sqlserverresultsetmetadata"></a>getColumnLabel 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取在打印输出和显示屏中使用的指定列的建议标题。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getColumnLabel(int column)  
```  
  
#### <a name="parameters"></a>Parameters  
 *column*  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 A**字符串**，其中包含的列标题。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSetMetaData 接口中的 getColumnLabel 方法指定此 getColumnLabel 方法。  
  
 此方法返回列的别名。 如果列别名不可用，此方法将返回列名称。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
