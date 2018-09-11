---
title: getCharacterStream 方法 (java.lang.String) |Microsoft Docs
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
- SQLServerResultSet.getCharacterStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cdddc572-05c1-480d-b3e5-28270001575c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8d1df393d88348a8645a78ecd11a170c8d9d746
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786774"
---
# <a name="getcharacterstream-method-javalangstring"></a>getCharacterStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称的值作为 java.io.Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getCharacterStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
## <a name="return-value"></a>返回值  
 一个读取器对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCharacterStream 方法由 java.sql.ResultSet 接口中的 getCharacterStream 方法指定。  
  
 此方法将只读取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Unicode 字符数据类型，例如 nchar、nvarchar、nvarchar(max) 和 ntext。 任何其他数据类型（包括 ASCII 字符类型）会引发异常。 若要读取 ASCII 数据类型，请使用 [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
