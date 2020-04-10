---
title: getBinaryStream 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.getBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c8f7741-daba-4c04-adc0-8d76345a899a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd4742b7c327899d8f3f7a0ce2a6d091a74eee03
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921671"
---
# <a name="getbinarystream-method-"></a>getBinaryStream 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个用于从 BLOB 中读取数据的输入流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getBinaryStream()  
```  
  
## <a name="return-value"></a>返回值  
 包含 BLOB 数据的输入流。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getBinaryStream 方法是由 java.sql.Blob 接口中的 getBinaryStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
