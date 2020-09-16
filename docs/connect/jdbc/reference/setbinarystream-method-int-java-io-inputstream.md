---
description: setBinaryStream 方法 (int, java.io.InputStream)
title: setBinaryStream 方法 (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c32b904-c44b-472e-a084-38f008a742b4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd868540d64b6d64146d5c69517c6b881abdb6de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432489"
---
# <a name="setbinarystream-method-int-javaioinputstream"></a>setBinaryStream 方法 (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的输入流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>参数  
 parameterIndex**  
  
 指示参数编号的 int****。  
  
 *x*  
  
 java.io.InputStream 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setBinaryStream 方法是由 java.sql.PreparedStatement 接口中的 setBinaryStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setBinaryStream 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
