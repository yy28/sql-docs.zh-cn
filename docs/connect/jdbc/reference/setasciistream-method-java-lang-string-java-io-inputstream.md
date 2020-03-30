---
title: 设置输入流的 setAsciiStream 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72da8111b115c9c1eda4a328fc2cc173eebea5c0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975442"
---
# <a name="setasciistream-method-javalangstring-javaioinputstream"></a>setAsciiStream 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的输入流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>parameters  
 parameterName   
  
 包含参数名称的字符串  。  
  
 *x*  
  
 InputStream 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setAsciiStream 方法是由 java.sql.PreparedStatement 接口中的 setAsciiStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setAsciiStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
