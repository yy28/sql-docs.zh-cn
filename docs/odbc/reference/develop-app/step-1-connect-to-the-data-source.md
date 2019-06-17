---
title: 第 1 步：连接到数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 154fdd7368835ba2a578d3ec641705c4064859ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149022"
---
# <a name="step-1-connect-to-the-data-source"></a>第 1 步：连接到数据源
任何应用程序的第一步是连接到数据源。 在下图中显示此阶段，包括它需要的函数。  
  
 ![连接到 ODBC 应用程序中的数据源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 连接到数据源的第一步是加载驱动程序管理器并分配环境句柄与**SQLAllocHandle**。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然后，应用程序注册到它通过调用符合的 ODBC 的版本**SQLSetEnvAttr** SQL_ATTR_APP_ODBC_VER 环境属性。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)并[向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下来，应用程序分配连接句柄与**SQLAllocHandle**并将连接到数据源**SQLConnect**， **SQLDriverConnect**，或者**SQLBrowseConnect**。 有关详细信息，请参阅[分配连接处理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)并[建立的连接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然后，应用程序设置的任何连接属性，如是否手动提交事务。 有关详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。
