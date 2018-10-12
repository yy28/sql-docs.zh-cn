---
title: getSubString 方法 (SQLServerNClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1d91c930-1bac-4da9-b9a5-ac2cfd31541b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f283115f4629e778d9b6fc4a94ccaf85064da6c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648955"
---
# <a name="getsubstring-method-sqlservernclob"></a>getSubString 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据指定的起始位置和要复制的字符数在 NCLOB 中检索指定子字符串的副本。  
  
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
 一个**字符串**中的，指定子字符串，它是**NCLOB**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSubString 方法由 java.sql.NClob 接口中的 getSubString 方法指定。  
  
 尝试从 Null 或长度为零的 NCLOB 获取零个字符将返回空字符串。 尝试在长度为零的 NCLOB 中从除了位置 1 之外的其他位置获取任意长度的字符将引发位置异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
