---
title: setBlob 方法 (SQLServerPreparedStatement) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 218ff486-3f31-49e4-ad81-a423246a8307
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f95060f35c36bd6a704ad53939afeab4d02101a7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setblob-method-sqlserverpreparedstatement"></a>setBlob 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数设置为给定的 Blob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setBlob(int i,  
                          java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *我*  
  
 **Int** ，该值指示参数号。  
  
 *x*  
  
 一个 Blob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 setBlob 方法指定此 setBlob 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
