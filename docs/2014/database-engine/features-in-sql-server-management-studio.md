---
title: SQL Server Management Studio 中的功能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], about SQL Server Management Studio
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: e75504b9-7968-4e3b-8411-fd79fe09021e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 790e02374fe209576c963c5f1e9c6e63e8e2d16b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779785"
---
# <a name="features-in-sql-server-management-studio"></a>SQL Server Management Studio 中的功能
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包括以下常用功能：  
  
-   支持 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的多数管理任务。  
  
-   用于 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 管理和创作的单一集成环境。  
  
-   用于管理 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的对象的对话框，使用这些对话框可以立即执行操作、将操作发送到代码编辑器或将其编写为脚本以供以后执行。  
  
-   非模式以及大小可调的对话框允许在打开某一对话框的情况下访问多个工具。  
  
-   常用的计划对话框使您可以在以后执行管理对话框的操作。  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 环境之间导出或导入 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 服务器注册。  
  
-   保存或打印由 SQL Server Profiler 生成的 XML 显示计划或死锁文件，以后进行查看，或将其发送给管理员以进行分析。  
  
-   新的错误和信息性消息框提供了详细信息，使您可以向 [!INCLUDE[msCoName](../includes/msconame-md.md)] 发送有关消息的注释，将消息复制到剪贴板，还可以通过电子邮件轻松地将消息发送给支持组。  
  
-   集成的 Web 浏览器可以快速浏览 MSDN 或联机帮助。  
  
-   从网上社区集成帮助。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 教程可以帮助您充分利用许多新功能，并可以快速提高效率。  
  
-   具有筛选和自动刷新功能的新活动监视器。  
  
-   集成的数据库邮件接口。  
  
## <a name="new-scripting-capabilities"></a>新的脚本撰写功能  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的代码编辑器组件包含集成的脚本编辑器，用来撰写 [!INCLUDE[tsql](../includes/tsql-md.md)]、MDX、DMX 和 XML/A。 主要功能包括：  
  
-   工作时显示动态帮助以便快速访问相关的信息。  
  
-   一套功能齐全的模板可用于创建自定义模板。  
  
-   可以编写和编辑查询或脚本，而无需连接到服务器。  
  
-   支持撰写 SQLCMD 查询和脚本。  
  
-   用于查看 XML 结果的新接口。  
  
-   用于解决方案和脚本项目的集成源代码管理，随着脚本的演化可以存储和维护脚本的副本。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 用于 MDX 语句的 IntelliSense 支持。  
  
## <a name="object-explorer-features"></a>对象资源管理器功能  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的对象资源管理器组件是一种集成工具，可以查看和管理所有服务器类型的对象。 主要功能包括：  
  
-   按完整名称或部分名称、架构或日期进行筛选。  
  
-   异步填充对象，并可以根据对象的元数据筛选对象。  
  
-   访问复制服务器上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理以进行管理。  
  
 有关详细信息，请参阅 [对象资源管理器](../ssms/object/object-explorer.md)。  
  
## <a name="extensibility"></a>扩展性  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 建立在 Visual Studio 隔离的 Shell 上，该 Shell 本身就支持扩展性（外接程序/插件）。 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]内可能引入 Visual Studio 扩展性服务来提供自定义功能，但是不支持这样的扩展性。  
  
 有一些用户和第三方开发了 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的扩展。 虽然我们没有对其进行禁止，但是请注意，我们不支持这种扩展性，因此可能存在向后/向前兼容性问题。 Microsoft 不会发布扩展 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的文档。 但是可利用社区博客和示例代码。  
  
 Microsoft 不支持将 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 与现有 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 扩展插件一起使用，因此如果您安装了 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 扩展插件，可能需要在就有关 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 问题致电 Microsoft 客户支持前删除这些插件。  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)  
  
  
