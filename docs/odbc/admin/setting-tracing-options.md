---
description: 设置跟踪选项
title: 设置跟踪选项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72e3805eded00b1bfa0c984d5ff0ace1ae1494fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476949"
---
# <a name="setting-tracing-options"></a>设置跟踪选项
通过 " **ODBC 数据源管理器**" 对话框的 "**跟踪**" 选项卡，您可以配置跟踪 ODBC 函数调用的方式。  
  
## <a name="how-tracing-works"></a>跟踪的工作原理  
 从 " **跟踪** " 选项卡启动跟踪时，驱动程序管理器将记录所有后续运行的应用程序的所有 ODBC 函数调用。 在开始跟踪之前，不会记录正在运行的应用程序的 ODBC 函数调用。 ODBC 函数调用记录在指定的日志文件中。  
  
 仅在单击 " **立即停止跟踪**" 后才停止跟踪。 请记住，跟踪打开时，日志文件将继续增加，这会影响所有 ODBC 应用程序的性能。  
  
 有关跟踪的详细信息，请参阅 [跟踪](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 跟踪中的更改  
 在 MDAC 2.7 SP2 之前，只允许在计算机范围内进行 ODBC 跟踪，在这种情况下，跟踪将捕获有关在任何标识下运行的所有 ODBC 应用程序的详细信息。 这包括对与 ODBC 相关的活动的跟踪，这些活动可能在代表其他本地用户帐户和内置安全主体（如本地服务和网络服务）创建或运行的过程中发生。  
  
 默认情况下，ODBC 跟踪现在使用每用户模式。 但是，如果您是本地管理员，则仍可以使用 ODBC 数据源管理器启用计算机范围的跟踪。  
  
 若要配置 ODBC 跟踪模式：  
  
1.  如果需要，请使用具有本地管理员组成员身份的帐户登录。  
  
2.  从 "管理工具" 中，打开 "ODBC 数据源管理器"。  
  
3.  单击“跟踪”选项卡。  
  
4.  使用 " **所有用户标识的计算机范围跟踪** " 复选框配置跟踪模式：  
  
5.  若要启用计算机范围跟踪，请选中该复选框。  
  
6.  若要返回到每用户跟踪，请清除该复选框。  
  
7.  单击“应用”。  
  
> [!NOTE]  
>  如果已在一种模式下启动跟踪，则必须停止跟踪，并切换到另一种模式，以使模式成功更改。  
  
> [!IMPORTANT]  
>  只应在需要时才启用计算机范围内的跟踪;否则，应关闭该功能。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 跟踪  
  
> [!IMPORTANT]  
>  从 Windows 8 (中开始，从 Windows 8 Visual Studio Analyzer 中删除了对 Visual Studio Analyzer 的支持，只包含在较早版本的 Visual Studio 中 ) 。 有关备用故障排除机制，请使用投标跟踪。  
  
 Visual Studio®分析器跟踪提供有关 ODBC 层的性能和调试信息。 所有传出事件都将在顶级接口上触发，以尽可能准确地显示有关 ODBC 组件所用时间的图片。 Visual Studio Analyzer 跟踪要求在设置源时注册任何事件源。 有关此类跟踪的详细信息，请参阅 Visual Studio 文档。
