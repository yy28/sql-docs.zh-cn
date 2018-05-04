---
title: ODBC 和标准 CLI |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2335d0eb5033ca6b32130503b4bd9a11f180c9c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和标准 CLI
ODBC 对齐具有以下规范和处理的调用级界面 (CLI) 标准。 （ODBC 功能是每个这些标准的超集。）  
  
-   Open Group CAE 规范"数据管理： SQL 调用级界面 (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) 调用级接口 (SQL/CLI)  
  
 由于此对齐方式，符合以下条件：  
  
-   应用程序写入到 Open Group 和 ISO CLI 规范将适用于 ODBC 3。*x*驱动程序或符合标准的驱动程序时使用 ODBC 3 编译。*x*标头文件，并与 ODBC 3 链接。*x*库，当它获取对通过 ODBC 3 驱动程序访问权限。*x*驱动程序管理器。  
  
-   写入到 Open Group 和 ISO CLI 规范的驱动程序会使用 ODBC 3 *.x*应用程序或一个符合标准的应用程序时使用 ODBC 3 编译 *.x*标头文件和链接ODBC 3 *.x*库，并当应用程序获得到通过 ODBC 3 驱动程序的访问权限 *.x*驱动程序管理器。 (有关详细信息，请参阅[符合标准的应用程序和驱动程序](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心接口一致性级别包括 ISO CLI 中的所有功能以及打开组 CLI 中的所有必需功能。 打开组 CLI 的可选功能，将显示在更高版本的界面一致性级别。 因为所有 ODBC 3。*x*驱动程序所需的核心接口一致性级别中功能的支持，满足以下条件：  
  
-   一个 ODBC 3。*x*驱动程序将支持符合标准的应用程序使用的所有功能。  
  
-   一个 ODBC 3。*x*使用仅 ISO CLI 中的功能和打开组 CLI 的必需功能的应用程序会使用任何符合标准的驱动程序。  
  
 除了包含 ISO/IEC 和打开组 CLI 标准中的调用级接口规范，ODBC 实现以下功能。 （其中，某些功能的版本中存在 ODBC 3 之前的 ODBC。*x*。)  
  
-   通过单个函数调用的多行提取  
  
-   绑定到的参数数组  
  
-   书签支持包括提取的书签、 可变长度书签和大容量更新和删除书签不连续的行上的操作  
  
-   按行绑定  
  
-   绑定偏移量  
  
-   对于在存储过程或作为一系列，通过执行 SQL 语句的 SQL 语句的批处理支持**SQLExecute**或**SQLExecDirect**  
  
-   准确或近似光标行计数  
  
-   函数调用通过定位更新和删除操作批处理的更新和删除 (**SQLSetPos**)  
  
-   从无需支持信息架构视图的信息架构中提取信息的目录函数  
  
-   外部联接、 标量函数、 日期时间文本、 间隔字符串和存储的过程的转义序列  
  
-   代码页转换库  
  
-   对驱动程序的 ANSI 一致性级别和 SQL 支持的报告  
  
-   按需自动填充的实现参数描述符  
  
-   增强的诊断和行和参数状态数组  
  
-   Datetime、 间隔、 数字/小数和 64 位整数应用程序缓冲区类型  
  
-   异步执行  
  
-   存储的过程支持，包括转义序列，输出参数绑定机制，以及目录函数  
  
-   连接增强功能包括支持连接属性和属性浏览
