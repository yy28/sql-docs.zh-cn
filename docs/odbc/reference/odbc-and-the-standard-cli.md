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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305138"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和标准 CLI
ODBC 与处理调用级别接口（CLI）的以下规范和标准保持一致。 （ODBC 功能是每种标准的超集。）  
  
-   开放式组 CAE 规范 "数据管理： SQL 调用级别接口（CLI）"  
  
-   ISO/IEC 9075-3:1995 （E）调用级别接口（SQL/CLI）  
  
 由于这种对齐方式的原因，以下是真实情况：  
  
-   当*使用 odbc 1.x 标头*文件编译和*链接 odbc 1.x 库，* 以及通过 Odbc *1.x 驱动程序*管理器获得对驱动程序的访问权限时，写入到开放组和 ISO CLI 规范的应用程序将*使用 odbc 1.x 驱动程序或*符合标准的驱动程序。  
  
-   当使用 odbc 1.x 标头文件编译和*链接 odbc 1.x*库时，以及当应用程序*通过 odbc 1.X* *驱动程序*管理器获得对驱动程序的访问权限时，写入到开放组和 ISO CLI 规范的驱动程序将*使用 odbc 1.x*应用程序或符合标准的应用程序。 （有关详细信息，请参阅[符合标准的应用程序和驱动程序](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心接口一致性级别包含了 ISO CLI 中的所有功能和开放组 CLI 中的所有 nonoptional 功能。 打开的组 CLI 的可选功能以更高的接口一致性级别显示。 由于支持核心接口一致性级别的功能需要*所有 ODBC 1.x*驱动程序，因此满足以下条件：  
  
-   ODBC 2.x 驱动程序将支持符合标准的*应用程序所*使用的所有功能。  
  
-   仅使用 ISO CLI 中的功能和开放组 CLI 的 nonoptional 功能的 ODBC 1.x 应用程序将适用于任何符合标准的*驱动程序。*  
  
 除了 ISO/IEC 和开放组 CLI 标准中包含的调用级别接口规范外，ODBC 还实现以下功能。 （其中一些功能存在于 ODBC 1.x 之前*的 odbc 版本中。）*  
  
-   单个函数调用的多行提取  
  
-   绑定到参数数组  
  
-   书签支持包括按书签、可变长度书签进行提取，以及通过对不连续行使用书签操作进行批量更新和删除  
  
-   按行绑定  
  
-   绑定偏移量  
  
-   支持批处理 SQL 语句，无论是在存储过程中还是通过**SQLExecute**或**SQLExecDirect**执行的一系列 sql 语句。  
  
-   确切或大致的游标行计数  
  
-   定位更新和删除操作以及按函数调用的批处理更新和删除（**SQLSetPos**）  
  
-   目录函数，从信息架构中提取信息，无需支持信息架构视图  
  
-   外部联接、标量函数、日期时间文本、间隔文本和存储过程的转义序列  
  
-   代码页翻译库  
  
-   报告驱动程序的 ANSI 一致性级别和 SQL 支持  
  
-   实现参数描述符的按需自动填充  
  
-   增强的诊断和行和参数状态阵列  
  
-   Datetime、interval、numeric/decimal 和64位整数应用程序缓冲区类型  
  
-   异步执行  
  
-   存储过程支持，包括转义序列、输出参数绑定机制和目录函数  
  
-   连接增强功能，包括对连接属性和属性浏览的支持
