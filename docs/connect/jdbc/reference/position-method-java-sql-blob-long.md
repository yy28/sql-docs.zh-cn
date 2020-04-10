---
title: position 方法 (java.sql.Blob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (java.sql.Blob.long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70fd642677405adf98cce23826775a0cab45221a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923183"
---
# <a name="position-method-javasqlblob-long"></a>position 方法 (java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的模式和起始索引返回 BLOB 中指定模式的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>parameters  
 *pattern*  
  
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
  
  
