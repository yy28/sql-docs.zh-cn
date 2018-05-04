---
title: 使用 32 位驱动程序的 32 位应用程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfffd8474f11c0e10fe521e9ea222c72127a6d63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>使用 32 位驱动程序的 32 位应用程序
你可以使用 32 位驱动程序运行 32 位应用程序。 32 位应用程序和 32 位驱动程序使用 Win32® API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了 32 位应用程序与 32 位驱动程序通信。 在应用程序调用 32 位驱动程序管理器，反过来调用 32 位驱动程序。  
  
 ![如何 32&#45;与 32 位应用程序通信&#45;位驱动程序](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  不要在 windows Nt/windows2000 本机上使用 32 位形式转换安装程序 DLL。 尽管它具有与 32 位安装程序 DLL 文件同名，它是一个不同的 DLL。  
  
## <a name="administration"></a>管理  
 你可以通过使用 ODBC 数据源管理器管理 32 位驱动程序的数据源。 若要打开 ODBC 管理器在运行 Windows 2000 的计算机上，打开 Windows 控制面板中，双击**管理工具**，然后双击**数据源 (ODBC)**。 运行以前版本的 Microsoft Windows 计算机上，名为图标**32 位 ODBC**或只需**ODBC**。  
  
## <a name="components"></a>Components  
 ODBC 组件包括以下文件运行 32 位驱动程序的 32 位应用程序。 这些组件是 \Redist 目录中。  
  
|文件名|Description|  
|---------------|-----------------|  
|所用的 Odbc32.dll|32 位驱动程序管理器|  
|Odbccp32.dll|32 位安装程序 DLL|  
|Odbcad32.exe|32 位 ODBC 管理器程序|  
|Odbcinst.hlp|安装程序帮助文件|  
|Msvcrt40.dll|C 运行时库|
