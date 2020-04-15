---
title: 第 1 步：连接到数据源 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a104733c0e5ec5acc87eeabd00c4e51d4bfd000
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301347"
---
# <a name="step-1-connect-to-the-data-source"></a>步骤 1：连接数据源
任何应用程序的第一步是连接到数据源。 此阶段（包括所需的功能）如下图所示。  
  
 ![连接到 ODBC 应用程序中的数据源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 连接到数据源的第一步是加载驱动程序管理器，并使用**SQLAllocHandle**分配环境句柄。 有关详细信息，请参阅[分配环境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然后，应用程序通过将**SQLSetEnvAttr**与SQL_ATTR_APP_ODBC_VER环境属性调用，注册其符合的 ODBC 版本。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下来，应用程序使用**SQLAllocHandle**分配连接句柄，并通过**SQLConnect、SQLDriverConnect**或**SQLDriverConnect** **SQLBrowseConnect**连接到数据源。 有关详细信息，请参阅[分配连接句柄](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)和[建立连接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然后，应用程序设置任何连接属性，例如是否手动提交事务。 有关详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。
