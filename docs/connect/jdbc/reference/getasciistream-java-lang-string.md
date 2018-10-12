---
title: getAsciiStream (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getAsciiStream(String paramName)
apilocation:
- SQLServerCallableStatement.getAsciiStream(String paramName)
apitype: Assembly
ms.assetid: 630b659f-eb36-4277-b04e-9a2e6134f795
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4169a8e4ec46993dd58c705b04b8f3e46b57892a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687525"
---
# <a name="getasciistream-javalangstring"></a>getAsciiStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称检索指定参数作为 ASCII 字符流的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.io.InputStream getAsciiStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>Parameters  
 paramName  
  
 指示参数名称的 String。  
  
## <a name="return-value"></a>返回值  
 InputStream 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另请参阅  
 [getAsciiStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
