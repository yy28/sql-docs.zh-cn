---
title: getAsciiStream 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getAsciiStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2d24a6b-f029-4691-981b-125c690b8ba5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: feadeaffb5fd74ebc6b2d273dca263cac16c14ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954197"
---
# <a name="getasciistream-method-javalangstring"></a>getAsciiStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称作为 ASCII 字符流的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getAsciiStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个 InputStream 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getAsciiStream 方法由 getAsciiStream 方法在方法中指定。  
  
## <a name="see-also"></a>另请参阅  
 [getAsciiStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
