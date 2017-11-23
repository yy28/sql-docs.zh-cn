---
title: "步骤 1： 连接到数据源 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 65c33be649b1c8007eef9e43db44897053a83a42
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="step-1-connect-to-the-data-source"></a>步骤 1： 连接到数据源
在任何应用程序中的第一步是将连接到数据源。 下图中显示此阶段中，包括它需要的函数。  
  
 ![连接到 ODBC 应用程序中的数据源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 连接到数据源的第一步是加载驱动程序管理器并分配与环境句柄**SQLAllocHandle**。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然后，应用程序注册到它通过调用符合的 ODBC 的版本**SQLSetEnvAttr**具有 SQL_ATTR_APP_ODBC_VER 环境属性。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下来，应用程序分配连接句柄与**SQLAllocHandle**并连接到数据源**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**。 有关详细信息，请参阅[分配连接处理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)和[建立的连接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然后，应用程序设置的任何连接属性，例如是否手动提交的事务。 有关详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。
