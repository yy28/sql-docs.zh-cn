---
title: setBoolean 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setBoolean
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8cd810b1-9858-4e51-9535-239d864cd288
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04f09bcd843946763fe3bb2b69cbdcd9560e7c91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975046"
---
# <a name="setboolean-method-sqlservercallablestatement"></a>setBoolean 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 boolean  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setBoolean(java.lang.String sCol,  
                       boolean b)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *b*  
  
 **布尔**值,**为 true**或**false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setBoolean 方法由 java.sql.CallableStatement 接口中的 setBoolean 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
