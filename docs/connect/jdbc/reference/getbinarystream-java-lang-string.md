---
title: getBinaryStream (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBinaryStream(String paramName)
apilocation:
- SQLServerCallableStatement.getBinaryStream(String paramName)
apitype: Assembly
ms.assetid: 17f1ea5d-47f8-4a66-a0fc-d6554b8e3866
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b450cd6a925aa5543262d70714cd36749113ed03
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953719"
---
# <a name="getbinarystream-javalangstring"></a>getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称检索指定参数的值作为无中断字节的二进制流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.io.InputStream getBinaryStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>parameters  
 paramName   
  
 指示参数名称的字符串  。  
  
## <a name="return-value"></a>返回值  
 InputStream 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另请参阅  
 [getBinaryStream 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
