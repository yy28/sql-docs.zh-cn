---
description: setBlob 方法 (SQLServerPreparedStatement)
title: setBlob 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 218ff486-3f31-49e4-ad81-a423246a8307
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a2ceade5959294d7ef4ae926a665bea9cd586fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432409"
---
# <a name="setblob-method-sqlserverpreparedstatement"></a>setBlob 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 Blob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setBlob(int i,  
                          java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>参数  
 *i*  
  
 指示参数编号的 int****。  
  
 *x*  
  
 Blob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setBlob 方法是由 java.sql.PreparedStatement 接口中的 setBlob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
