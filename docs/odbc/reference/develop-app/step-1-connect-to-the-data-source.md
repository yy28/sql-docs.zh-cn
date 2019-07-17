---
title: 步骤 1：连接到数据源 |Microsoft Docs
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
ms.openlocfilehash: 80f2dfc05d9d27f60aca414ee0abd13e13b3ea65
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114271"
---
# <a name="step-1-connect-to-the-data-source"></a>步骤 1：连接到数据源
任何应用程序的第一步是连接到数据源。 在下图中显示此阶段，包括它需要的函数。  
  
 ![连接到 ODBC 应用程序中的数据源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 连接到数据源的第一步是加载驱动程序管理器并分配环境句柄与**SQLAllocHandle**。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然后，应用程序注册到它通过调用符合的 ODBC 的版本**SQLSetEnvAttr** SQL_ATTR_APP_ODBC_VER 环境属性。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)并[向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下来，应用程序分配连接句柄与**SQLAllocHandle**并将连接到数据源**SQLConnect**， **SQLDriverConnect**，或者**SQLBrowseConnect**。 有关详细信息，请参阅[分配连接处理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)并[建立的连接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然后，应用程序设置的任何连接属性，如是否手动提交事务。 有关详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。
