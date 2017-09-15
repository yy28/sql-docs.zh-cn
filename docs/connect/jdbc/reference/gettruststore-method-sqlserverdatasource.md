---
title: "getTrustStore 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e23a59adeb94be0f7cacebdc40fb442c3c69f9ae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回指向证书 trustStore 文件的路径（包括文件名）。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**，它包含的证书信任库文件或为 null （包括文件名称） 路径，如果未不设置任何值。  
  
## <a name="remarks"></a>注释  
 如果未设置 trustStore 属性， [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)方法将返回 null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
