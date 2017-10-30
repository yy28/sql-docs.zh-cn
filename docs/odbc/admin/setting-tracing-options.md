---
title: "设置跟踪选项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b11d6337c2e0ca2853838d964842be536454c5f4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setting-tracing-options"></a>设置跟踪选项
**跟踪**选项卡**ODBC 数据源管理器**对话框中，可以配置跟踪 ODBC 函数调用的方法。  
  
## <a name="how-tracing-works"></a>跟踪的工作原理  
 当启动跟踪**跟踪**选项卡上，驱动程序管理器将记录所有 ODBC 函数调用，所有随后运行应用程序。 不会记录跟踪启动之前已运行的应用程序从 ODBC 函数调用。 ODBC 函数调用会记录在你指定的日志文件。  
  
 跟踪将停止，仅在您单击后**立即停止跟踪**。 请记住，跟踪时，日志文件将继续增加，这会影响所有 ODBC 应用程序的性能。  
  
 有关跟踪的详细信息，请参阅[跟踪](../../odbc/reference/develop-app/tracing.md)。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 跟踪中的更改  
 MDAC 2.7 SP2 之前, 仅允许 ODBC 跟踪发生在计算机范围内，在其中跟踪捕获有关的所有标识下运行的所有 ODBC 应用程序公开的详细信息。 这包括创建或代表其他本地用户帐户和内置安全主体，如本地服务和网络服务运行的进程可能会出现的与 ODBC 相关的活动的跟踪。  
  
 默认情况下，ODBC 跟踪现在使用每个用户模式。 如果你是本地管理员，但是，可以通过使用 ODBC 数据源管理器仍启用计算机范围跟踪。  
  
 若要配置 ODBC 跟踪模式：  
  
1.  如果有必要，在使用具有本地管理员组成员身份的帐户登录。  
  
2.  从管理工具中，打开 ODBC 数据源管理器。  
  
3.  单击**跟踪**选项卡。  
  
4.  配置跟踪模式使用**所有用户标识的计算机范围跟踪**复选框：  
  
5.  要启用计算机范围跟踪，选中复选框。  
  
6.  若要返回到每个用户跟踪，请清除复选框。  
  
7.  单击 **“应用”**。  
  
> [!NOTE]  
>  如果你已经开始跟踪在一种模式中，你必须停止跟踪并切换到要成功更改的模式的其他模式。  
  
> [!IMPORTANT]  
>  需要; 时，才应启用计算机范围跟踪否则，应留关闭。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 跟踪  
  
> [!IMPORTANT]  
>  Windows 8 （Visual Studio Analyzer 仅包含在较旧版本的 Visual Studio。） 从开始已删除的 Visual Studio Analyzer 的支持。 有关故障排除机制的替代方法，使用 BID 跟踪。  
  
 Visual Studio® 分析器跟踪提供性能和有关 ODBC 层的调试信息。 传出的所有事件将都激发顶级接口形式显示准确图片尽可能 ODBC 组件所用相关的时间。 Visual Studio Analyzer 跟踪需要时源设置注册任何事件源。 有关这种类型的跟踪的详细信息，请参阅 Visual Studio 文档。

