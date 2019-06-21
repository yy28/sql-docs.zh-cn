---
title: getBinaryStream 方法 (long，long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30bc8882-04b4-4efd-95e4-7d3a2a8c1d47
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e78a745e908399efa25e6f72faff9daec2cbd8ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799789"
---
# <a name="getbinarystream-method-long-long"></a>getBinaryStream 方法 (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  通过使用指定的起始位置和长度来返回包含部分 BLOB 值的输入流对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getBinaryStream(long pos, long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 pos   
  
 要检索的部分值的第一个字节的偏移量。  
  
 *length*  
  
 要检索的部分值的字节长度。  
  
## <a name="return-value"></a>返回值  
 包含 BLOB 数据的输入流。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBinaryStream 方法由 java.sql.Blob 接口中的 getBinaryStream 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
