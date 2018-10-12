---
title: setByte 方法 (SQLServerCallableStatement) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5149bbd4e1bf85f4a1e1e7ff923f59d1578814de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667775"
---
# <a name="setbyte-method-sqlservercallablestatement"></a>setByte 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 byte 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setByte(java.lang.String sCol,  
                    byte b)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
 *b*  
  
 一个 byte 值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setByte 方法是由 java.sql.CallableStatement 接口中的 setByte 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
