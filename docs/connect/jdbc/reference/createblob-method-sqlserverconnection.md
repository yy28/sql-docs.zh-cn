---
title: createBlob 方法 (SQLServerConnection) | Microsoft Docs
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
ms.openlocfilehash: 3d70c72b860044a7e61b4a6dc5474c465fb60e89
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67955404"
---
# <a name="createblob-method-sqlserverconnection"></a>createBlob 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建不含任何数据的 Blob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Blob createBlob()  
```  
  
## <a name="return-value"></a>返回值  
 Blob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 createBlob 方法是由 java.sql.Connection 接口中的 createBlob 方法指定的。  
  
 此方法取代了对 [SQLServerBlob 构造函数（SQLServerConnection、byte）](../../../connect/jdbc/reference/sqlserverblob-constructor-sqlserverconnection-byte.md)的需求。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
