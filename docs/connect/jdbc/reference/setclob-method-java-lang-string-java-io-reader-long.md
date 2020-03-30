---
title: setClob 方法 (java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bc9fddea-134e-4440-ba54-a1f74bb40c46
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98069f3b907d923a7eeca295b1c2a0d983c2edc1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974553"
---
# <a name="setclob-method-javalangstring-javaioreader-long"></a>setClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为具有指定字符数长度的指定 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.io.Reader value,  
            long length)  
```  
  
#### <a name="parameters"></a>parameters  
 parameterName   
  
 包含参数名称的字符串  。  
  
 *value*  
  
 Reader 对象。  
  
 *length*  
  
 指示流中字符数的 long  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setClob 方法是由 java.sql.CallableStatement 接口中的 setClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
