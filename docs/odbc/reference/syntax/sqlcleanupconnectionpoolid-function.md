---
title: "SQLCleanupConnectionPoolID 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49d204d7d77ae39c6a7eb3c9d408f6d72bafcc91
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函数
**一致性**  
 版本引入了： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**通知的驱动程序池 ID 已超时。池 ID 可以超时，每当中具有该池 ID 相关联的池的所有连接都已超时。请参阅[Microsoft 数据访问组件中的池](http://msdn.microsoft.com/library/ms810829.aspx)有关连接超时的详细信息。  
  
## <a name="syntax"></a>语法  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>参数  
 *EnvironmentHandle*  
 [输入]池的环境句柄。  
  
 *池 Id*  
 [输入]操作已超时的池 id 相关联的池。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 驱动程序管理器将不会处理从返回的诊断信息**SQLCleanupConnectionPoolID**。  
  
 应用程序无法接收由驱动程序返回的错误消息。  
  
## <a name="remarks"></a>注释  
 **SQLCleanupConnectionPoolID**可以调用任何时候，但驱动程序管理器可保证其他任何线程都同时调用**SQLGetPoolID**和其他任何线程都同时调用**SQLRateConnection**和**SQLPoolConnect**与连接信息令牌分配有该池 id。 因此，该驱动程序必须确保此函数是线程安全。  
  
 驱动程序可以清除与池 id。 关联的资源  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [开发中的 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

