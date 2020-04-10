---
title: setBinaryStream 方法 (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d4dd274fd77de831f2ea7484cc759ab4cb771d7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928840"
---
# <a name="setbinarystream-method-sqlserverblob"></a>setBinaryStream 方法 (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可用于写入 BLOB 值的流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>parameters  
 Pos   
  
 BLOB 值中开始写入的位置。  
  
## <a name="return-value"></a>返回值  
 输出流。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>备注  
 此 setBinaryStream 方法是由 java.sql.Blob 接口中的 setBinaryStream 方法指定的。  
  
 输出流从指定位置开始覆盖 BLOB 中的数据，并可以超过 BLOB 的初始长度。 指定“位置+1”值将追加字节。 传递“位置+2”或更大值（或零或更小值）会引发位置错误。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
