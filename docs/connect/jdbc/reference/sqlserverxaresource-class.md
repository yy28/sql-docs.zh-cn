---
title: SQLServerXAResource 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 575982cd29c949203fdd667230cb8cad8d79f774
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784265"
---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示用于 XA 分布式事务管理的 XAResource。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.lang.Object  
  
 **实现：** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Remarks  
 通过使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式事务管理器 (DTC) 在 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 中实现 XA 事务。 SQLServerXAResource 类调用名为 sqljdbc_xa.dll 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 扩展 dll，此 dll 充当 DTC 接口。 SQLServerXAResource 接收到的 XA 调用（XA_START、XA_END、XA_PREPARE 等）将映射到针对 DTC 函数的相应调用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
