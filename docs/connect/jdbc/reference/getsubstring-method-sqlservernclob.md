---
title: "getSubString 方法 (SQLServerNClob) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d91c930-1bac-4da9-b9a5-ac2cfd31541b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4e6593a2eba1d1a0bef3dfca5477d96c990c7f10
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getsubstring-method-sqlservernclob"></a>getSubString 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定的子字符串内的副本**NCLOB**基于指定的起始位置和要复制的字符数。  
  
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
 A**字符串**，它是指定的子字符串中**NCLOB**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.NClob 接口中的 getSubString 方法指定此 getSubString 方法。  
  
 尝试从 Null 或长度为零的 NCLOB 获取零个字符将返回空字符串。 尝试在长度为零的 NCLOB 中从除了位置 1 之外的其他位置获取任意长度的字符将引发位置异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

