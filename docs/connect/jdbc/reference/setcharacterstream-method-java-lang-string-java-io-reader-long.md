---
title: setCharacterStream 方法 （java.lang.String，java.io.Reader，长） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 54fb2f13-f8d8-47b5-bec1-4a5af3e86a84
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4253de4038b1505a3befdbbf80f47c9f210735ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-long"></a>setCharacterStream 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数设置为指定的 java.io.Reader 对象，它是指定的字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *参数名称*  
  
 包含参数名称的字符串。  
  
 *读取器*  
  
 一个包含 Unicode 数据的读取器对象。  
  
 *length*  
  
 A**长**，该值指示流中的字符数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 setCharacterStream 方法指定此 setCharacterStream 方法。  
  
 流的长度是否不同于中指定了什么*长度*参数，在更新或插入行时的 JDBC 驱动程序引发异常。  
  
 如果流的长度为未知，*长度*参数可能设置为-1，以指示该驱动程序应接受而不考虑其长度流。 与 sqljdbc4.jar，我们建议你使用 JDBC 4.0 方法[setCharacterStream 方法 （java.lang.String，java.io.Reader）](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md)当应用程序希望更新的列从一个流，其长度为未知。  
  
## <a name="see-also"></a>另请参阅  
 [setCharacterStream 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
