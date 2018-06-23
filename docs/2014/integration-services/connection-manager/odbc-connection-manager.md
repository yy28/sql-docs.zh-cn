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
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9453dc6e402fce60e1f4f440d84f882e513abea7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027719"
---
# <a name="odbc-connection-manager"></a>ODBC 连接管理器
  ODBC 连接管理器使得包能够使用开放式数据库连接规范 (ODBC) 连接到多种数据库管理系统。  
  
 当您添加到包的 ODBC 连接并设置连接管理器属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建连接管理器，并将添加到连接管理器`Connections`包的集合。 该连接管理器在运行时决定物理 ODBC 连接。  
  
 `ConnectionManagerType`的连接管理器的属性设置为`ODBC`。  
  
 可以用下列方式配置 ODBC 连接管理器：  
  
-   提供引用用户名或系统数据源名称的连接字符串。  
  
-   指定要连接的服务器。  
  
-   指示在运行时是否保留连接。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>配置 ODBC 连接管理器  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [ODBC 连接管理器 UI 参考](../odbc-connection-manager-ui-reference.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[添加连接以编程方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;连接](integration-services-ssis-connections.md)  
  
  