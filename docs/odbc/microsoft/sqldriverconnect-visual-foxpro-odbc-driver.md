---
description: SQLDriverConnect（Visual FoxPro ODBC 驱动程序）
title: SQLDriverConnect (Visual FoxPro ODBC 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc985a5a56f54b1af8f9153bcd5129523233e2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421791"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别1  
  
 连接到现有数据源，该数据源可以是 [数据库](../../odbc/microsoft/visual-foxpro-terminology.md) 或 [可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录。 ODBC 属性关键字 UID 和 PWD 将被忽略。 下表列出了其他支持的属性关键字。  
  
|ODBC attribute 关键字|特性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|被 Visual FoxPro ODBC 驱动程序忽略，但不生成错误。|  
|PWD|被 Visual FoxPro ODBC 驱动程序忽略，但不生成错误。|  
|驱动程序|Visual FoxPro ODBC 驱动程序的名称和位置;由驱动程序管理器实现。|  
  
|Visual FoxPro ODBC Driver attribute 关键字|特性值|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"是" 或 "否"|  
|逐份打印|"计算机" 或其他排序序列。 有关支持的排序规则的列表，请参阅 [设置整理](../../odbc/microsoft/set-collate-command.md)。|  
|描述||  
|排他|"是" 或 "否"|  
|SourceDB|包含零个或多个 [自由表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录的完全限定路径，或者 [数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的绝对路径和文件名。|  
|SourceType|"DBC" 或 "DBF"|  
|版本||  
  
 如果未指定数据源名称，则驱动程序管理器将根据 *fDriverCompletion* 参数的设置提示用户输入 (信息) 然后继续。 如果需要详细信息，Visual FoxPro ODBC 驱动程序将显示提示对话框。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 。
