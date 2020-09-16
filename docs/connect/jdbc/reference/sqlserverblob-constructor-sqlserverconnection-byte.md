---
description: SQLServerBlob 构造函数 (SQLServerConnection, byte)
title: SQLServerBlob 构造函数 (SQLServerConnection, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 968c32094196c88ab8eb607e6faa8992de40ed00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472159"
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob 构造函数 (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在给定 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象和字节数组时，初始化 [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) 类的新实例****。  
  
> [!NOTE]  
>  JDBC 驱动程序 2.0 版已不推荐使用此方法， 而是使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>参数  
 连接  
  
 SQLServerConnection 对象。  
  
 *data*  
  
 一个字节数组****。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerBlob 构造函数](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
