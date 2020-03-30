---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd2208d2a82a9376438b61e144665cbda5152bb8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975057"
---
# <a name="setblob-method-sqlserverpreparedstatement"></a>setBlob 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 Blob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setBlob(int i,  
                          java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>parameters  
 *i*  
  
 指示参数编号的 int  。  
  
 *x*  
  
 Blob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setBlob 方法是由 java.sql.PreparedStatement 接口中的 setBlob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
