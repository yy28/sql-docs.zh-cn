---
title: 跟踪 DLL |微软文档
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
ms.openlocfilehash: 8e1f9dc57415ad9865ca1b2ad02487b62a93f18f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298067"
---
# <a name="trace-dll"></a>跟踪 DLL
执行跟踪的 DLL 是 ODBC 核心组件之一。 跟踪 DLL 当前作为示例 DLL 在 Windows SDK 的 ODBC 组件中提供，并且以前包括 Microsoft 数据访问组件 （MDAC） SDK。 因此，跟踪 DLL 的注册表项、接口和示例代码可用。 此 DLL 可以替换为由 ODBC 用户或第三方供应商生成的跟踪 DLL。 应为自定义跟踪 DLL 指定与原始示例跟踪 DLL 不同的名称。 跟踪 DLL 必须安装在系统目录中，否则将无法加载。 驱动程序管理器不会将连接字符串传递到跟踪 DLL。  
  
 跟踪 DLL 跟踪输入参数、输出参数、延迟参数、返回代码和 SQLSTAT。 启用跟踪后，Driver Manager 将在两个点调用跟踪 DLL：一次在函数条目（参数验证之前），另一次在函数返回之前调用。  
  
 当应用程序调用函数时，驱动程序管理器在调用驱动程序中的函数或处理调用本身之前，在跟踪 DLL 中调用跟踪函数。 每个 ODBC 函数都有一个相应的跟踪函数（以*跟踪*为预缀），该函数与 ODBC 函数相同，但名称除外。 调用跟踪函数时，跟踪 DLL 捕获输入参数并返回返回代码。 由于在驱动程序管理器验证参数之前调用了跟踪 DLL，因此将跟踪无效的函数调用，因此记录状态转换错误和无效参数。  
  
 在跟踪 DLL 中调用跟踪函数后，驱动程序管理器在驱动程序中调用 ODBC 函数。 然后在跟踪 DLL 中调用**跟踪返回**。 此函数采用两个参数：跟踪函数的跟踪 DLL 返回的值，以及驱动程序返回到 ODBC 函数的驱动程序管理器的返回代码（或者驱动程序管理器本身处理该函数时返回的值）。 函数使用为跟踪函数返回的值来操作捕获的输入参数值。 它将为 ODBC 函数返回的代码写入日志文件（如果启用，则动态显示）。 它取消引用输出参数指针并记录输出参数值。
