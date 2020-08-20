---
description: 跟踪 DLL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1791b72b5f7e836fba05275f87bd57948a273775
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487500"
---
# <a name="trace-dll"></a>跟踪 DLL
执行跟踪的 DLL 是一个 ODBC 核心组件。 跟踪 DLL 目前作为 Windows SDK 的 ODBC 组件中的示例 DLL 提供，以前曾包含 Microsoft 数据访问组件 (MDAC) SDK。 因此，可以使用跟踪 DLL 的注册表项、接口和示例代码。 此 DLL 可由 ODBC 用户或第三方供应商生成的跟踪 DLL 替换。 应为自定义跟踪 DLL 提供不同于原始示例跟踪 DLL 的名称。 跟踪 Dll 必须安装在系统目录中，否则无法加载。 驱动程序管理器将不向跟踪 DLL 传递连接字符串。  
  
 跟踪 DLL 跟踪输入参数、输出参数、延迟参数、返回代码和 SQLSTATEs。 启用跟踪时，驱动程序管理器将在两个点调用跟踪 DLL：一次是在参数) 验证之前 (函数入口，在函数返回之前再次出现。  
  
 当应用程序调用函数时，驱动程序管理器会在调用驱动程序中的函数或处理调用本身之前，在跟踪 DLL 中调用跟踪函数。 每个 ODBC 函数都有一个对应的 trace 函数 (前缀为 *跟踪*) ，该函数与具有相同名称的 ODBC 函数相同。 调用 trace 函数时，跟踪 DLL 捕获输入参数并返回一个返回代码。 由于在驱动程序管理器验证参数之前调用跟踪 DLL，因此跟踪无效的函数调用，因此会记录无效的状态转换错误和无效参数。  
  
 在跟踪 DLL 中调用 trace 函数之后，驱动程序管理器将调用驱动程序中的 ODBC 函数。 然后，它调用跟踪 DLL 中的 **TraceReturn** 。 此函数采用两个参数： trace DLL 为 trace 函数返回的值，并将驱动程序返回的返回代码返回给 ODBC 函数的驱动程序管理器 (或由驱动程序管理器本身返回的值（如果它处理函数) ）。 函数使用为 trace 函数返回的值来操作捕获的输入参数值。 如果已启用) ，它会将 ODBC 函数的返回代码写入日志文件 (或动态显示该文件。 它取消引用输出参数指针并记录输出参数值。
