---
title: updateClob 方法 （java.lang.String，java.io.Reader，长） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b8f759a-ce5d-41b2-b6cc-24a3ab299f1f
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25ddba644335a47aba33889600330e1988905c47
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="updateclob-method-javalangstring-javaioreader-long"></a>updateClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的具有指定数量字符的 Reader 对象更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 A**字符串**包含列标签。  
  
 *读取器*  
  
 一个读取器对象。  
  
 *length*  
  
 参数数据中的字符数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateClob 方法指定此 updateClob 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateClob 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
