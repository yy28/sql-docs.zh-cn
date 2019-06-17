---
title: createBlob 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 630a93b0-6e3c-4255-a007-1097ce0ee243
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 38c4ccf19e42946506b274cdef2058726ccfe407
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768257"
---
# <a name="createblob-method-sqlserverconnection"></a>createBlob 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建不含任何数据的 Blob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Blob createBlob()  
```  
  
## <a name="return-value"></a>返回值  
 一个 Blob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 createBlob 方法由 java.sql.Connection 接口中的 createBlob 方法指定。  
  
 此方法无需[SQLServerBlob 构造函数&#40;SQLServerConnection，byte&#41;](../../../connect/jdbc/reference/sqlserverblob-constructor-sqlserverconnection-byte.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
