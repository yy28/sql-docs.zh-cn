---
title: 16 位应用程序使用 32 位驱动程序 |Microsoft 文档
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
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8be9b55137ebbfd0da4a4194b3f29ea57fb89d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905482"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>16 位应用程序使用 32 位驱动程序
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 改为使用 32 位或 64 位驱动程序管理器。  
  
 你可以运行 16 位应用程序与 32 位驱动程序基于 Windows 的系统上，只要 32 位驱动程序不显式调用创建线程的 Win32 API 函数。 Windows (WOW) 子系统上的 Windows 在 16 位模式下运行应用程序，并解析到操作系统的 16 位调用。 ODBC 形式转换为 32 位驱动程序的应用程序 Dll 解析 16 位调用。 16 位应用程序使用 Windows API 中，和 32 位驱动程序使用 Win32 API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了如何 16 位应用程序与 32 位驱动程序通信。 16 位驱动程序管理器和 32 位驱动程序之间是通用的形式转换转换为 32 位 ODBC 调用的 16 位 ODBC 调用的 Dll。  
  
 ![如何 16&#45;与 32 位应用程序通信&#45;位驱动程序](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  将 16 位应用程序交互使用 32 位驱动程序，每当 32 位驱动程序管理器将始终返回"2.0"作为 ODBC 版本驱动程序支持。  
  
## <a name="administration"></a>管理  
 你可以通过使用 ODBC 数据源管理器管理 32 位驱动程序的数据源。 若要打开 ODBC 管理器运行 Microsoft® Windows® 2000年的计算机上，打开 Windows 控制面板中，双击**管理工具**，然后双击**数据源 (ODBC)**。 运行以前版本的 Microsoft Windows 计算机上，名为图标**32 位 ODBC**或只需**ODBC**。  
  
 下图显示的 16 位应用程序如何调用 32 位驱动程序安装程序 DLL。 16 位安装程序 DLL 之间的 32 位驱动程序安装程序 DLL 是将转换的 16 位安装程序对 32 位安装程序 DLL 调用的 DLL 调用的泛型形式转换 DLL。  
  
 ![如何 16&#45;位应用程序调用 32&#45;位驱动程序安装程序 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 Windows 中 （形式转换为 32 位的 16 位） 的 Windows 上，名为 Ds32gt.dll 转换为 16 位自变量值传递 32 位安装程序的其他形式转换 DLL DLL 回 16 位。  
  
## <a name="components"></a>Components  
 MDAC 2.8 SP1 SDK 的 ODBC 组件包括以下文件运行 32 位驱动程序的 16 位应用程序。 这些组件是 \Redist 目录中。  
  
|文件名|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|16 位 ODBC 泛型形式转换 DLL|  
|Odbc32gt.dll|32 位 ODBC 泛型形式转换 DLL|  
|Odbccp32.dll|32 位安装程序 DLL|  
|Odbcad32.exe|32 位管理员程序|  
|Odbcinst.hlp|安装程序帮助文件|  
|Ds16gt.dll|泛型形式 DLL 转换的 16 位驱动程序安装程序|  
|Ctl3d32.dll|32 位三维窗口样式库|  
  
 此外，不是 ODBC 3.51 的一部分，以及 16 位 ODBC 2.10 驱动程序管理器中的以下文件所需的并且应与 16 位应用程序安装。  
  
|文件名|Description|  
|---------------|-----------------|  
|Odbc.dll|16 位驱动程序管理器|  
|Odbcinst.dll|16 位安装程序 DLL|  
|Odbcadm.exe|16 位 ODBC 管理器程序|
