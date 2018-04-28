---
title: 截断方法 (SQLServerBlob) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerBlob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ef181e04-003a-442a-9b7e-0c508a7cc873
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78f58fd0e0c7730927ce370abc2099c797bc24ee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="truncate-method-sqlserverblob"></a>truncate 方法 (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将一个 BLOB，给定长度的截断。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parameters  
 len  
  
 BLOB 的新长度。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 java.sql.Blob 接口中的截断方法指定此截断的方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
