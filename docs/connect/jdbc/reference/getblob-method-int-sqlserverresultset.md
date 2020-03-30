---
title: getBlob 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBlob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a00275cb-0299-4a21-a518-2640598a5bbf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70f0faaa9babb4ddaa1512fd18cbbd1f5f34d337
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67953600"
---
# <a name="getblob-method-int-sqlserverresultset"></a>getBlob 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 Java 编程语言中的 Blob 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Blob getBlob(int i)  
```  
  
#### <a name="parameters"></a>parameters  
 *i*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 Blob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getBlob 方法是由 java.sql.ResultSet 接口中的 getBlob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBlob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
