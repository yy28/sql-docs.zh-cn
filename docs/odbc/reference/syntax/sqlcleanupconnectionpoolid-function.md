---
title: SQLCleanup 连接池 ID 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a74a92cc05ecd41e99ff87642c7fe3ee527e0c98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301317"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函数
**一致性**  
 版本介绍： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**通知驱动程序池 ID 已超时。每当与该池 ID 关联的池中的所有连接超时时，池 ID 都可以超时。有关连接超时的详细信息，请参阅[Microsoft 数据访问组件中的池](https://msdn.microsoft.com/library/ms810829.aspx)。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>参数  
 *环境处理*  
 [输入]池的环境句柄。  
  
 *池 ID*  
 [输入]与超时的池 ID 关联的池。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 驱动程序管理器不会处理从**SQLCleanupConnection 池 ID**返回的诊断信息。  
  
 应用程序无法接收驱动程序返回的错误消息。  
  
## <a name="remarks"></a>备注  
 **SQLCleanupConnectionPoolID**可以随时调用，但驱动程序管理器保证没有其他线程同时调用**SQLGetPoolID，** 并且没有其他线程同时使用该池 ID 分配的连接信息令牌调用**SQLRateConnection**和**SQLPoolConnect。** 因此，驱动程序必须确保此函数是线程安全的。  
  
 驱动程序可以清理与池 ID 关联的资源。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
