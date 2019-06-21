---
title: getBytes 方法 (SQLServerBlob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9686d29f11f2357b983dce349e8e4dc5d13af664
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66804013"
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
 pos   
  
 开始位置，从 1（而不是从 0）开始。  
  
 *length*  
  
 要获取的数据的长度。  
  
## <a name="return-value"></a>返回值  
 包含请求数据的 byte  数组。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBytes 方法是由 java.sql.Blob 接口中的 getBytes 方法指定的。  
  
 如果具有长度为 Null 或为零的 BLOB，并试图在位置 1 处获取恰好零字节，此时将返回空的 byte  数组（长度为 0 的字节数组）。  
  
 如果具有长度为 Null 或为零的 BLOB，并试图从位置 1 之外的其他位置获取任意长度的字节，此时将引发位置异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
