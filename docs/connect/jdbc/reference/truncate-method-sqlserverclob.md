---
title: truncate 方法 (SQLServerClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5535cbc5d2417cfabfba1a3a001deee2ec27fe5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615435"
---
# <a name="truncate-method-sqlserverclob"></a>truncate 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将 CLOB 截断为给定的长度。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parameters  
 len  
  
 CLOB 应截断为的长度（以字符数表示）。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此截断方法由 java.sql.Clob 接口中的截断方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
