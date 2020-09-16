---
description: setString 方法 (SQLServerPreparedStatement)
title: setString 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 25dabdc9-c60f-485a-87eb-306067964765
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71517999110a0b7f41f2ceac5eae409d57ce0f1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450716"
---
# <a name="setstring-method-sqlserverpreparedstatement"></a>setString 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 String **** 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setString(int index,  
                            java.lang.String str)  
```  
  
#### <a name="parameters"></a>参数  
 *index*  
  
 指示参数编号的 int****。  
  
 *str*  
  
 一个字符串值****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setString 方法是由 java.sql.PreparedStatement 接口中的 setString 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
