---
title: 步骤1：连接到数据源 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114271"
---
# <a name="step-1-connect-to-the-data-source"></a>步骤 1：连接数据源
任何应用程序的第一步是连接到数据源。 下图显示了此阶段（包括它需要的函数）。  
  
 ![连接到 ODBC 应用程序中的数据源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 连接到数据源的第一步是加载驱动程序管理器，并通过**SQLAllocHandle**分配环境句柄。 有关详细信息，请参阅[分配环境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然后，应用程序通过使用 SQL_ATTR_APP_ODBC_VER 环境属性调用**SQLSetEnvAttr** ，来注册它所符合的 ODBC 版本。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下来，应用程序使用**SQLAllocHandle**分配连接句柄，并使用**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**连接到数据源。 有关详细信息，请参阅[分配连接句柄](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)和[建立连接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然后，应用程序会设置任何连接属性，如是否手动提交事务。 有关详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。
