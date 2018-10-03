---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ccf5afd559d4d3716c22b42665c516aa230fafe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626576"
---
# <a name="setting-tracing-options"></a>设置跟踪选项
**跟踪**选项卡**ODBC 数据源管理器**对话框可以配置跟踪 ODBC 函数调用的方法。  
  
## <a name="how-tracing-works"></a>跟踪的工作原理  
 当开始从跟踪**跟踪**选项卡上，驱动程序管理器将记录所有 ODBC 函数调用的所有随后运行的应用程序。 不记录跟踪启动之前运行的应用程序的 ODBC 函数调用。 ODBC 函数调用记录在您指定的日志文件中。  
  
 跟踪仅在单击后将停止**立即停止跟踪**。 请记住，跟踪时，日志文件将继续增加，这会影响所有 ODBC 应用程序的性能。  
  
 有关跟踪的详细信息，请参阅[跟踪](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>在 ODBC 跟踪更改  
 MDAC 2.7 SP2 之前的 ODBC 跟踪是仅允许发生在计算机范围内，在其中跟踪将捕获有关任何标识下运行的所有 ODBC 应用程序公开的详细信息。 这包括对可能出现的创建或代表其他本地用户帐户和内置安全主体，如本地服务和网络服务运行的进程的有关 ODBC 的活动的跟踪。  
  
 默认情况下，ODBC 跟踪现在使用每个用户模式。 如果您是本地管理员，但是，可以通过使用 ODBC 数据源管理器仍启用计算机范围内跟踪。  
  
 若要配置 ODBC 跟踪模式：  
  
1.  如果有必要，在使用具有本地管理员组成员身份的帐户登录。  
  
2.  从管理工具，打开 ODBC 数据源管理器。  
  
3.  单击**跟踪**选项卡。  
  
4.  配置跟踪模式下使用**所有的用户标识的计算机范围内跟踪**复选框：  
  
5.  若要启用计算机范围内跟踪，请选择该复选框。  
  
6.  若要返回到每个用户跟踪，请清除该复选框。  
  
7.  单击 **“应用”**。  
  
> [!NOTE]  
>  如果已有一种模式中启动跟踪，必须停止跟踪并切换到要成功更改的模式的其他模式。  
  
> [!IMPORTANT]  
>  需要; 时，才应启用计算机范围内跟踪否则，应留处于关闭状态。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio 分析器跟踪  
  
> [!IMPORTANT]  
>  在 Windows 8 中 （Visual Studio 分析器仅包含在较旧版本的 Visual Studio。） 开始已不再对 Visual Studio 分析器的支持。 有关故障排除机制的替代方法，使用 BID 跟踪。  
  
 Visual Studio® 分析器跟踪提供性能和关于 ODBC 层的调试信息。 所有传出事件将触发在顶级的接口，以便将为准确图片尽可能所用的 ODBC 组件相关的时间。 Visual Studio 分析器跟踪需要时在源设置注册任何事件源。 有关跟踪此类的详细信息，请参阅 Visual Studio 文档。
