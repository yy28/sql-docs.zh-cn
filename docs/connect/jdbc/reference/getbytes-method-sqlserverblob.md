---
title: "getBytes 方法 (SQLServerBlob) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerBlob.getBytes
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c6125a23f0c66e7e24533cacf1ce77d829003ce8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getbytes-method-sqlserverblob"></a>getBytes 方法 (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取 BLOB 数据作为字节数组。  
  
## <a name="syntax"></a>语法  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 开始位置，从 1（而不是从 0）开始。  
  
 *length*  
  
 要获取的数据的长度。  
  
## <a name="return-value"></a>返回值  
 A**字节**数组，其中包含所请求的数据。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Blob 接口中的 getBytes 方法指定此 getBytes 方法。  
  
 如果你具有 null 或零长度 BLOB，并尝试在位置 1，空获取完全零字节**字节**（字节数组的长度为 0），则返回数组。  
  
 如果具有长度为 Null 或为零的 BLOB，并试图从位置 1 之外的其他位置获取任意长度的字节，此时将引发位置异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
