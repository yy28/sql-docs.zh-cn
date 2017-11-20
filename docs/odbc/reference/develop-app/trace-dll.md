---
title: "跟踪 DLL |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 22bbb28f42f7bd3c1ec32e01c3451944315861a0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="trace-dll"></a>跟踪 DLL
执行跟踪的 DLL 是 ODBC 核心组件之一。 以前，的跟踪 DLL 作为 Windows SDK 的 ODBC 组件中的示例 DLL 当前提供，已包括 Microsoft 数据访问组件 (MDAC) SDK。 因此，注册表项、 接口和跟踪 DLL 的示例代码将可用。 可以由跟踪由 ODBC 用户或第三方供应商的 DLL 替换此 DLL。 自定义跟踪 DLL 应不同于原始示例跟踪 DLL 的名称。 跟踪 Dll 必须安装在系统目录中，否则它们将无法加载。 连接字符串将不会传递到跟踪 DLL 的驱动程序管理器。  
  
 跟踪 DLL 跟踪输入自变量、 输出自变量、 延迟的自变量、 返回代码和 SQLSTATEs。 当启用了跟踪时，驱动程序管理器将调用跟踪 DLL，在两个点： 一次在函数入口 （之前参数验证），再次只是该函数将返回之前。  
  
 当应用程序调用一个函数时，驱动程序管理器跟踪在驱动程序中调用函数或处理调用本身之前的 DLL 中调用跟踪函数。 每个 ODBC 函数有一个相应的跟踪函数 (前缀为*跟踪*) 与 ODBC 函数除名称外完全相同。 当调用跟踪函数时，跟踪 DLL 捕获的输入的参数和返回的返回代码。 因为跟踪 DLL 称为之前驱动程序管理器验证自变量，无效的函数调用跟踪，以便记录状态转换错误和无效自变量。  
  
 在调用之后跟踪函数跟踪 DLL 中，驱动程序管理器调用 ODBC 函数驱动程序中。 然后，它调用**TraceReturn**跟踪 DLL 中。 此函数采用两个参数： 跟踪 DLL 对于跟踪函数中，返回的值并返回由驱动程序到驱动程序管理器 ODBC 函数的返回代码 （或如果它处理了该函数返回由驱动程序管理器本身的值）。 该函数使用跟踪函数返回的值捕获的输入的参数值进行操作。 它将写入到日志文件 ODBC 函数返回的代码 （或动态，显示它，如果启用）。 它输出自变量指针取消引用和日志的输出参数值。

