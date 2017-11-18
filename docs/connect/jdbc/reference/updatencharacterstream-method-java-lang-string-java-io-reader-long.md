---
title: "updateNCharacterStream 方法字符串读取器的长) |Microsoft 文档"
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
ms.assetid: db0a96a8-248f-4664-9c13-f480f309ab91
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3dc6bb87cb7539fb6060e2affbe0622a0d94cc6f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updatencharacterstream-method-javalangstring-javaioreader-long"></a>updateNCharacterStream 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将具有指定字节数的字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNCharacterStream(java.lang.String columnLabel,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 A**字符串**包含列标签。  
  
 *读取器*  
  
 一个读取器对象。  
  
 *length*  
  
 流的长度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateNCharacterStream 方法指定此 updateNCharacterStream 方法。  
  
 此方法将从读取器对象，选择传递 Unicode 字符**nchar**， **nvarchar (max)**， **ntext**，和**xml**列。 在其他数据类型列上使用此方法会引发异常。  
  
 流的长度是否不同于中指定了什么*长度*参数，在更新或插入行时的 JDBC 驱动程序引发异常。  
  
 如果流的长度为未知，*长度*参数可能设置为-1，以指示该驱动程序应接受而不考虑其长度流。 与 sqljdbc4.jar，我们建议你使用 JDBC 4.0 方法[updateNCharacterStream 方法 &#40;java.lang.String、 java.io.Reader &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-java-lang-string-java-io-reader.md)当应用程序希望更新的列从一个流，其长度为未知。  
  
## <a name="see-also"></a>另请参阅  
 [updateNCharacterStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

