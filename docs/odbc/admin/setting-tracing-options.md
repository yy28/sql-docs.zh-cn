---
title: 设置跟踪选项 |微软文档
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
ms.openlocfilehash: 21bee5d903459423a134389e62db844f5f63c9c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307189"
---
# <a name="setting-tracing-options"></a>设置跟踪选项
**通过"ODBC 数据源管理员"** 对话框的 **"跟踪"** 选项卡，您可以配置跟踪 ODBC 函数调用的方式。  
  
## <a name="how-tracing-works"></a>跟踪的工作原理  
 从 **"跟踪"** 选项卡开始跟踪时，驱动程序管理器将记录所有随后运行的应用程序的所有 ODBC 函数调用。 不会记录在开始跟踪之前运行的应用程序的 ODBC 函数调用。 ODBC 函数调用记录在您指定的日志文件中。  
  
 仅在单击"**立即停止跟踪"后才会停止。** 请记住，当跟踪打开时，日志文件继续增加，这会影响所有 ODBC 应用程序的性能。  
  
 有关跟踪的详细信息，请参阅[跟踪](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 跟踪的变化  
 在 MDAC 2.7 SP2 之前，ODBC 跟踪只允许在全机范围内进行，跟踪捕获任何标识下运行的所有 ODBC 应用程序的公开详细信息。 这包括跟踪可能针对代表其他本地用户帐户和内置安全主体（如本地服务和网络服务）创建或运行的进程发生的与 ODBC 相关的活动。  
  
 默认情况下，ODBC 跟踪现在使用每个用户模式。 但是，如果您是本地管理员，您仍可以使用 ODBC 数据源管理员启用计算机范围的跟踪。  
  
 要配置 ODBC 跟踪模式：  
  
1.  如有必要，请使用本地管理员组中具有成员资格的帐户登录。  
  
2.  从管理工具中，打开 ODBC 数据源管理员。  
  
3.  单击“跟踪”**** 选项卡。  
  
4.  使用"**机器范围跟踪"配置跟踪模式，以检查所有用户身份**复选框：  
  
5.  要启用机器范围的跟踪，请选择该复选框。  
  
6.  要返回到每个用户跟踪，请清除该复选框。  
  
7.  单击 **“应用”**。  
  
> [!NOTE]  
>  如果已在一种模式下开始跟踪，则必须停止跟踪并切换到其他模式才能成功更改模式。  
  
> [!IMPORTANT]  
>  仅当需要时才应启用机器范围的跟踪;否则，它应该关闭。  
  
## <a name="visual-studio-analyzer-tracing"></a>可视化工作室分析器跟踪  
  
> [!IMPORTANT]  
>  从 Windows 8 开始删除了对可视化工作室分析器的支持（视觉工作室分析器仅包含在旧版本的 Visual Studio 中）。 对于其他故障排除机制，请使用 BID 跟踪。  
  
 可视化 Studio®分析器跟踪提供有关 ODBC 层的性能和调试信息。 所有传出事件都将在顶级界面触发，以尽可能准确地显示 ODBC 组件所花费的时间。 可视化工作室分析器跟踪需要设置源时注册任何事件源。 有关此类跟踪的详细信息，请参阅 Visual Studio 文档。
