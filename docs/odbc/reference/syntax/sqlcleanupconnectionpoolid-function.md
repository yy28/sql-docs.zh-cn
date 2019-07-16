---
title: SQLCleanupConnectionPoolID 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee8f9b9879a3533e8196bbc89f8ae0b0a132293a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036096"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函数
**符合性**  
 版本引入了：ODBC 3.81 标准符合性：ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**通知池 ID 已超时的驱动程序。池 ID 可以超时，只要中具有该池 ID 相关联的池的所有连接都已超时。请参阅[Microsoft 数据访问组件中的池](https://msdn.microsoft.com/library/ms810829.aspx)连接超时值有关的详细信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>参数  
 *EnvironmentHandle*  
 [输入]池的环境句柄。  
  
 *PoolID*  
 [输入]操作已超时的池 id 相关联的池。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 驱动程序管理器不会处理从返回的诊断信息**SQLCleanupConnectionPoolID**。  
  
 应用程序不能接收由驱动程序返回的错误消息。  
  
## <a name="remarks"></a>备注  
 **SQLCleanupConnectionPoolID**可能会调用在任何时候，但是，驱动程序管理器保证没有其他线程同时调用**SQLGetPoolID**并没有其他线程同时调用**SQLRateConnection**并**SQLPoolConnect**与连接信息令牌分配有该池 id。 因此，该驱动程序必须确保此函数是线程安全。  
  
 驱动程序可以清理池 id。 与关联的资源  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
