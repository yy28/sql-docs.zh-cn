---
title: getSubString 方法 (SQLServerClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cecfab59bc318d2ce6a2061e2116f5523b9874d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652225"
---
# <a name="getsubstring-method-sqlserverclob"></a>getSubString 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的起始位置和要复制的字符数返回 CLOB 中指定子字符串的副本。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 要提取的子字符串的第一个字符。 第一个字符的位置为 1。  
  
 *length*  
  
 要复制的连续字符数。  
  
## <a name="return-value"></a>返回值  
 指示 CLOB 中指定子字符串的 String 值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSubString 方法由 java.sql.Clob 接口中的 getSubString 方法指定。  
  
 尝试从 Null 或长度为零的 CLOB 获取零个字符将返回空字符串。 尝试在长度为零的 CLOB 中从除了位置 1 之外的其他位置获取任意长度的字符将引发位置异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
