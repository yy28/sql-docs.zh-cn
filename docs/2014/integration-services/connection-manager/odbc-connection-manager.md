---
title: ODBC 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e0b8bb7a7a2b32f2566a725842919f0260c3f78
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267133"
---
# <a name="odbc-connection-manager"></a>ODBC 连接管理器
  ODBC 连接管理器使得包能够使用开放式数据库连接规范 (ODBC) 连接到多种数据库管理系统。  
  
 将 ODBC 连接添加到包并设置连接管理器属性时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接管理器，并将添加到连接管理器`Connections`包的集合。 该连接管理器在运行时决定物理 ODBC 连接。  
  
 `ConnectionManagerType`连接管理器属性设置为`ODBC`。  
  
 可以用下列方式配置 ODBC 连接管理器：  
  
-   提供引用用户名或系统数据源名称的连接字符串。  
  
-   指定要连接的服务器。  
  
-   指示在运行时是否保留连接。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>配置 ODBC 连接管理器  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [ODBC 连接管理器 UI 参考](../odbc-connection-manager-ui-reference.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>并[连接以编程方式添加](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;的连接](integration-services-ssis-connections.md)  
  
  
