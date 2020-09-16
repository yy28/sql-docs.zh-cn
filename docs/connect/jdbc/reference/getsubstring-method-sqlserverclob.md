---
description: getSubString 方法 (SQLServerClob)
title: getSubString 方法 (SQLServerClob) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd407745df5e07ae2265105f990aa9df2a4ec963
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434309"
---
# <a name="getsubstring-method-sqlserverclob"></a>getSubString 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的起始位置和要复制的字符数返回 CLOB 中指定子字符串的副本。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>参数  
 pos  
  
 要提取的子字符串的第一个字符。 第一个字符的位置为 1。  
  
 *length*  
  
 要复制的连续字符数。  
  
## <a name="return-value"></a>返回值  
 指示 CLOB 中指定子字符串的 String**** 值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getSubString 方法是由 java.sql.Clob 接口中的 getSubString 方法指定的。  
  
 尝试从 Null 或长度为零的 CLOB 获取零个字符将返回空字符串。 尝试在长度为零的 CLOB 中从除了位置 1 之外的其他位置获取任意长度的字符将引发位置异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
