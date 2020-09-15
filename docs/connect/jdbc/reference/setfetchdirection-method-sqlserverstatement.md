---
description: setFetchDirection 方法 (SQLServerStatement)
title: setFetchDirection 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9469fe9b0e559358e3e18c15719161b0ae0033
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431869"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>setFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  为 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供提示以指明处理结果集行时应采用的方向。  
  
> [!NOTE]  
>  JDBC 驱动程序目前忽略了此方法给出的提示。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>参数  
 nDir**  
  
 指示行处理方向的 int****，可以为以下值之一：  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setFetchDirection 方法是由 java.sql.Statement 接口中的 setFetchDirection 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
