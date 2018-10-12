---
title: setShort 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setShort
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d7031a89-e964-4ffd-87b7-63825799435d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33d39d7e0242ff7913fd13858cd35fc81ea6858c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662235"
---
# <a name="setshort-method-sqlservercallablestatement"></a>setShort 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 short 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setShort(java.lang.String sCol,  
                     short s)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的 String。  
  
 *s*  
  
 一个 **short** 值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setShort 方法是由 java.sql.CallableStatement 接口中的 setShort 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
