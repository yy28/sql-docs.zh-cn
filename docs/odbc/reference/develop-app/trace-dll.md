---
title: 跟踪 DLL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fe910c93beac676e5fb0f663b740c03a826c326
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985226"
---
# <a name="trace-dll"></a>跟踪 DLL
执行跟踪的 DLL 是 ODBC 核心组件之一。 跟踪 DLL 作为 Windows SDK 的 ODBC 组件中的示例 DLL 当前提供和了以前包含 Microsoft 数据访问组件 (MDAC) SDK。 因此，注册表项、 接口和跟踪 DLL 的示例代码都可用。 此 DLL 可由跟踪 DLL ODBC 用户或第三方供应商生成的替换。 应为自定义跟踪 DLL 提供不同于原始示例跟踪 DLL 的名称。 跟踪 Dll 必须安装在系统目录中，否则它们将无法加载。 连接字符串将不会传递到跟踪 DLL 由驱动程序管理器。  
  
 跟踪 DLL 跟踪输入的参数、 输出自变量、 延迟的参数、 返回代码和 SQLSTATEs。 驱动程序管理器启用跟踪后，调用跟踪 DLL 在两个点： 一次在函数入口 （之前参数验证），然后再次就该函数将返回之前。  
  
 当应用程序调用一个函数时，驱动程序管理器跟踪在驱动程序中调用函数或处理本身的调用之前的 DLL 中调用跟踪函数。 每个 ODBC 函数有一个相应的跟踪函数 (带有前缀*跟踪*) 这是除名称外的 ODBC 函数相同。 当调用跟踪函数时，跟踪 DLL 捕获的输入的参数和返回返回代码。 之前驱动程序管理器验证自变量调用跟踪 DLL，因为要跟踪无效的函数调用，因此记录状态转换错误和无效的参数。  
  
 在调用之后跟踪函数跟踪 DLL 中，驱动程序管理器调用驱动程序中的 ODBC 函数。 然后，它调用**TraceReturn**跟踪 DLL 中。 此函数采用两个参数： 跟踪 DLL 跟踪函数返回的值并返回由驱动程序的驱动程序管理器的 ODBC 函数的返回代码 （或如果处理该函数返回由驱动程序管理器本身的值）。 该函数使用的跟踪函数返回值来操作捕获的输入的参数值。 它将写入到日志文件的 ODBC 函数返回的代码 （或如果启用，则将其动态地显示）。 它输出自变量指针取消引用和日志输出自变量值。
