---
description: 配合使用 16 位和 32 位应用程序与 32 位驱动程序
title: 使用带有32位驱动程序的16位和32位应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3985fa6fa4fd24ad9638e418915542b48abc26f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471372"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>配合使用 16 位和 32 位应用程序与 32 位驱动程序
> [!IMPORTANT]  
>  在 Windows 的未来版本中将删除16位应用程序支持。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 改为开发32位或64位的应用程序。  
  
 使用 ODBC 数据访问组件，可以将16位和32位应用程序与32位驱动程序一起使用。 Microsoft® Windows®95/98 和 Microsoft Windows NT®/Windows 2000 操作系统支持以下应用程序和驱动程序的组合：  
  
-   带有32位驱动程序的16位应用程序  
  
-   32位驱动程序的32位应用程序  
  
 不支持将32位应用程序与16位驱动程序一起使用。  
  
> [!NOTE]  
>  从 ODBC 3.0 版开始，已支持 Windows NT 4.0。  
  
 ODBC 包括必要的 ODBC 组件，这些组件可通过 "thunk" 动态链接库 (Dll) 将16位地址转换为32位地址，反之亦然。 安装程序将确定正在使用的操作系统并安装该系统所需的 ODBC 组件。 你还可以选择安装所有系统使用的 ODBC 组件。  
  
 大多数情况下，将应用程序或驱动程序从16位移植到32位涉及五种类型的更改：  
  
-   对消息处理代码的更改  
  
-   由于整数和句柄为32位而发生的更改  
  
-   对 Windows 应用程序编程接口调用 (Api 的更改)   
  
-   将驱动程序设置为线程安全的更改  
  
-   对 ODBC 组件的更改  
  
 从应用程序或驱动程序的角度来看，16位和32位 ODBC 组件之间的主要区别在于它们具有不同的文件名。 从系统角度来看，每个应用程序或驱动程序连接的体系结构不同，用于管理数据源的工具是不同的。  
  
 本部分包含以下主题。  
  
-   [配合使用 16 位应用程序和 32 位驱动程序](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [配合使用 32 位应用程序和 32 位驱动程序](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
