---
title: ODBC 和标准 CLI |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5485da176b9bd4aa7afca7afa088e6932d6f0d58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273303"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和标准 CLI
ODBC 与以下的规范和处理使用调用级别接口 (CLI) 的标准保持一致。 （ODBC 功能是每个这些标准的超集。）  
  
-   打开组 CAE 规范"数据管理：SQL 调用级别接口 (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) 调用级别接口 (SQL/CLI)  
  
 由于这种调整，而满足以下条件：  
  
-   编写指向 Open Group 和 ISO CLI 规范的应用程序将使用 ODBC 3。*x*驱动程序或符合标准的驱动程序时使用 ODBC 3 编译。*x*标头文件，并与 ODBC 3 链接。*x*库，并当它获得通过 ODBC 3 驱动程序的访问权限。*x*驱动程序管理器。  
  
-   编写 Open Group 和 ISO CLI 规范的驱动程序将使用 ODBC 3 *.x*应用程序或符合标准的应用程序时使用 ODBC 3 编译 *.x*标头文件和链接ODBC 3 *.x*库，并当应用程序获得通过 ODBC 3 驱动程序的访问权限 *.x*驱动程序管理器。 (有关详细信息，请参阅[符合标准的应用程序和驱动程序](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心接口一致性级别包含 ISO CLI 中的所有功能和打开组 CLI 中的所有必需功能。 打开组 CLI 的可选功能，显示在更高版本的接口一致性级别。 因为所有 ODBC 3。*x*驱动程序以支持中核心接口一致性级别的功能，需要满足以下条件：  
  
-   ODBC 3。*x*驱动程序将支持符合标准的应用程序使用的所有功能。  
  
-   ODBC 3。*x*使用仅在 ISO CLI 中的功能和打开组 CLI 的必需功能的应用程序会使用任何符合标准的驱动程序。  
  
 除了调用级别接口规范包含 ISO/IEC 和打开组 CLI 标准中，ODBC 将实现以下功能。 （其中一些功能的版本中存在 ODBC 3 之前的 ODBC。*x*。)  
  
-   通过单个函数调用提取多行  
  
-   绑定到参数的数组  
  
-   书签支持包括提取的书签、 可变长度书签和大容量更新和删除的书签操作上不连续的行  
  
-   按行绑定  
  
-   绑定的偏移量  
  
-   对 SQL 语句，在存储过程中或作为一系列，通过执行 SQL 语句的批处理支持**SQLExecute**或**SQLExecDirect**  
  
-   准确或近似游标行计数  
  
-   定位更新和删除操作和批处理的更新和删除的函数调用 (**SQLSetPos**)  
  
-   从无需支持信息架构视图的信息架构中提取信息的目录函数  
  
-   外部联接、 标量函数、 日期时间文字，间隔文本和存储的过程的转义序列  
  
-   代码页转换库  
  
-   驱动程序的 ANSI 一致性级别和 SQL 支持的报告  
  
-   按需自动填充实现参数描述符  
  
-   增强的诊断和行和参数状态数组  
  
-   日期时间、 间隔、 数字/小数和 64 位整数应用程序缓冲区类型  
  
-   异步执行  
  
-   包括转义序列的存储的过程支持输出参数绑定机制，以及目录函数  
  
-   连接增强功能包括支持的连接属性和属性浏览
