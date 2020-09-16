---
description: setUnicodeStream 方法 (SQLServerPreparedStatement)
title: setUnicodeStream 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a413e83-e0a4-41f8-9fe0-33ce4d368ee4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: abcc41af7eedf01670aaaf439619e3fb199461c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467132"
---
# <a name="setunicodestream-method-sqlserverpreparedstatement"></a>setUnicodeStream 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数编号设置为将有指定字节数的给定输入流。  
  
> [!NOTE]  
>  此方法在 JDBC 规范中已不推荐使用，调用它将导致引发“尚未实现”异常。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setUnicodeStream(int n,  
                                   java.io.InputStream x,  
                                   int length)  
```  
  
#### <a name="parameters"></a>参数  
 *n*  
  
 指示参数编号的 int****。  
  
 *x*  
  
 InputStream 对象。  
  
 *length*  
  
 字节数。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setUnicodeStream 方法是由 java.sql.PreparedStatement 接口中的 setUnicodeStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
