---
title: setByte 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setByte
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0fbb03a5-61ee-4fb8-9dea-dce5cb1a367e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0039322a86e0dd35c0da78e3173f835bcc47129d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975013"
---
# <a name="setbyte-method-sqlservercallablestatement"></a>setByte 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 byte 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setByte(java.lang.String sCol,  
                    byte b)  
```  
  
#### <a name="parameters"></a>parameters  
 sCol  
  
 包含参数名称的字符串。  
  
 *b*  
  
 一个 byte 值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setByte 方法是由 java.sql.CallableStatement 接口中的 setByte 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
