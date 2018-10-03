---
title: 包执行和其他操作监视 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b985193eb9aa9b73d513f2d5ce8368f5d8fbb6ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060688"
---
# <a name="monitoring-for-package-executions-and-other-operations"></a>监视包执行和其他操作
  您可以使用以下一个或多个工具监视 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包执行、项目验证和其他操作。 某些工具（如数据分流）只适用于部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的项目。  
  
-   日志  
  
     有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](integration-services-ssis-logging.md)。  
  
-   报表  
  
     有关详细信息，请参阅 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)。  
  
-   视图  
  
     有关详细信息，请参阅[视图（Integration Services 目录）](/sql/integration-services/system-views/views-integration-services-catalog)。  
  
-   性能计数器  
  
     有关详细信息，请参阅 [性能计时器](performance-counters.md)。  
  
-   数据分流  
  
## <a name="operation-types"></a>操作类型  
 在中监视多个不同类型的操作`SSISDB`目录中[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服务器。 每个操作可以具有多个与其关联的消息。 每个消息可划分为若干不同类型之一。 例如，消息可以是信息、警告或错误类型。 有关消息类型的完整列表，请参阅针对 Transact-SQL [catalog.operation_messages（SSISDB 数据库）](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)视图的文档。 有关操作类型的完整列表，请参阅 [catalog.operations（SSISDB 数据库）](/sql/integration-services/system-views/catalog-operations-ssisdb-database)。  
  
 使用九种不同的状态类型来指示操作的状态。 有关状态类型的完整列表，请参阅 [catalog.operations（SSISDB 数据库）](/sql/integration-services/system-views/catalog-operations-ssisdb-database)视图。  
  
## <a name="related-content"></a>相关内容  
 blogs.msdn.com 上的博客文章 [SSIS T-SQL API 概述](http://go.microsoft.com/fwlink/?LinkId=249051)。  
  
  
