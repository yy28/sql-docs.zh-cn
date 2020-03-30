---
title: position 方法 (byte, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf8cfa3bb6aed74c7689639698715dc24803d46d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976472"
---
# <a name="position-method-byte-long"></a>position 方法 (byte, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的 byte  数组模式和起始索引返回 BLOB 中指定模式的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>parameters  
 bPattern   
  
 要搜索的模式。  
  
 *start*  
  
 要搜索的起始索引。  
  
## <a name="return-value"></a>返回值  
 指示找到模式的位置的 long  值，如果未找到，则为 -1。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 position 方法是由 java.sql.Blob 接口中的 position 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [position 方法 (SQLServerBlob)](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
