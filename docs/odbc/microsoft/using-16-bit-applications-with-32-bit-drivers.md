---
title: 使用 16 位应用程序和 32 位驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209978"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>配合使用 16 位应用程序和 32 位驱动程序
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 改为使用 32 位或 64 位驱动程序管理器。  
  
 您可以运行 16 位应用程序与 32 位驱动程序在基于 Windows 的系统上为 32 位驱动程序不显式调用创建的线程的 Win32 API 函数。 Windows (WOW) 子系统上的 Windows 在 16 位模式下运行的应用程序，并解决对操作系统的 16 位调用。 ODBC 形式转换为 32 位驱动程序的应用程序 Dll 解析 16 位调用。 16 位应用程序时使用 Windows API 和 32 位驱动程序使用 Win32 API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了 16 位应用程序与 32 位驱动程序进行通信。 16 位驱动程序管理器和 32 位驱动程序之间是通用的形式转换转换为 32 位 ODBC 调用的 16 位 ODBC 调用的 Dll。  
  
 ![如何 16&#45;具有 32 位应用程序的通信&#45;位驱动程序](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  只要一个 16 位应用程序与 32 位驱动程序进行交互，32 位驱动程序管理器将始终返回"2.0"作为版本的 ODBC 驱动程序支持。  
  
## <a name="administration"></a>管理  
 可以通过使用 ODBC 数据源管理器管理 32 位驱动程序的数据的源。 若要打开 ODBC 管理器中运行 Microsoft® Windows® 2000年的计算机上，打开 Windows 控制面板中，双击**管理工具**，然后双击**数据源 (ODBC)** 。 在计算机上运行的 Microsoft Windows 的早期版本，名为图标**32 位 ODBC**或只需**ODBC**。  
  
 下图显示了如何的 16 位应用程序调用 32 位驱动程序安装程序 DLL。 16 位安装程序 DLL 之间的 32 位驱动程序安装程序 DLL 是将转换为 32 位安装程序 DLL 调用的 16 位安装程序 DLL 调用的泛型形式转换 DLL。  
  
 ![如何 16&#45;位应用程序调用 32&#45;位驱动程序安装程序 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 Windows （形式转换为 32 位的 16 位） 的 Windows，名为 Ds32gt.dll 转换为 16 位自变量值传递 32 位安装程序的其他形式转换 DLL DLL 回 16 位。  
  
## <a name="components"></a>组件  
 MDAC 2.8 SP1 SDK 的 ODBC 组件包括以下文件为运行 32 位驱动程序使用 16 位应用程序。 这些组件是 \Redist 目录中。  
  
|File name|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|16 位 ODBC 泛型形式转换 DLL|  
|Odbc32gt.dll|32 位 ODBC 泛型形式转换 DLL|  
|Odbccp32.dll|32 位安装程序 DLL|  
|Odbcad32.exe|32 位管理程序|  
|Odbcinst.hlp|安装程序帮助文件|  
|Ds16gt.dll|16 位驱动程序安装程序泛型形式转换 DLL|  
|Ctl3d32.dll|32 位三维窗口样式库|  
  
 此外，以下文件以及 16 位 2.10 的 ODBC 驱动程序管理器中，这不是 ODBC 3.51 的一部分，所需的应使用 16 位应用程序安装。  
  
|File name|Description|  
|---------------|-----------------|  
|Odbc.dll|16 位驱动程序管理器|  
|Odbcinst.dll|16 位安装程序 DLL|  
|Odbcadm.exe|16 位 ODBC 管理器程序|
