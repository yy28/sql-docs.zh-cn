---
title: ODBC 和标准 CLI |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305138"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和标准 CLI
ODBC 符合与呼叫级接口 （CLI） 打交道的以下规范和标准。 （ODBC 功能是每个标准的超级集。  
  
-   打开组 CAE 规范"数据管理：SQL 调用级接口 （CLI）"  
  
-   ISO/IEC 9075-3：1995 （E） 呼叫级接口 （SQL/CLI）  
  
 由于这种对齐方式，以下情况为 true：  
  
-   写入 Open Group 和 ISO CLI 规范的应用程序在使用 ODBC *3.x*标头文件编译并与 ODBC *3.x*库链接时，以及通过 ODBC *3.x*驱动程序管理器访问驱动程序时，将使用 ODBC *3.x*驱动程序或符合标准的驱动程序。  
  
-   写入 Open Group 和 ISO CLI 规范的驱动程序在使用 ODBC *3.x*标头文件编译并与 ODBC *3.x*库链接时，以及当应用程序通过 ODBC *3.x*驱动程序管理器访问驱动程序时，它将与 ODBC *3.x*应用程序或符合标准的应用程序配合使用。 （有关详细信息，请参阅[符合标准的应用程序和驱动程序](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心接口一致性级别包含 ISO CLI 中的所有功能以及开放组 CLI 中的所有非可选功能。 开放组 CLI 的可选功能显示在更高的接口符合性级别中。 由于所有 ODBC *3.x*驱动程序都需要支持核心接口一致性级别的功能，因此如下所示：  
  
-   ODBC *3.x*驱动程序将支持符合标准的应用程序使用的所有功能。  
  
-   仅使用 ISO CLI 中的功能和开放组 CLI 的非可选功能的 ODBC *3.x*应用程序将与任何符合标准的驱动程序配合使用。  
  
 除了 ISO/IEC 和开放组 CLI 标准中包含的呼叫级接口规范外，ODBC 还实现了以下功能。 （其中一些功能存在于 ODBC *3.x*之前的 ODBC 版本中。  
  
-   通过单个函数调用获取多行  
  
-   绑定到参数数组  
  
-   书签支持，包括按书签提取、可变长度书签以及批量更新和删除不连续行上的书签操作  
  
-   行绑定  
  
-   绑定偏移  
  
-   支持批处理 SQL 语句，无论是在存储过程中，还是作为通过 SQLExecute 或**SQLExecDirect** **SQLExecDirect**执行的 SQL 语句序列  
  
-   精确或近似光标行计数  
  
-   定位更新和删除操作以及按函数调用 **（SQLSetPos）** 批处理更新和删除  
  
-   目录函数，无需支持信息架构视图，即可从信息架构中提取信息  
  
-   外部联接、标量函数、日期时间文本、间隔文本和存储过程的转义序列  
  
-   代码页翻译库  
  
-   报告驱动程序的 ANSI 符合性级别和 SQL 支持  
  
-   按需自动填充实现参数描述符  
  
-   增强的诊断以及行和参数状态数组  
  
-   日期时间、间隔、数字/十进制和 64 位整数应用程序缓冲区类型  
  
-   异步执行  
  
-   存储过程支持，包括转义序列、输出参数绑定机制和目录函数  
  
-   连接增强功能，包括支持连接属性和属性浏览
