---
title: setClob 方法 （java.lang.String，java.io.Reader，长） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bc9fddea-134e-4440-ba54-a1f74bb40c46
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2fb51dba5eee7258aaacabcc87f28042897a1f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setclob-method-javalangstring-javaioreader-long"></a>setClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数设置为指定的读取器对象是指定的字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.io.Reader value,  
            long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *参数名称*  
  
 包含参数名称的字符串。  
  
 *值*  
  
 一个读取器对象。  
  
 *length*  
  
 A**长**，该值指示流中的字符数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 setClob 方法指定此 setClob 方法。  
  
## <a name="see-also"></a>另请参阅  
 [setClob 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
