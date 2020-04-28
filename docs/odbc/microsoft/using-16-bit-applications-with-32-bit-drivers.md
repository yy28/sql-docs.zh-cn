---
title: 使用带有32位驱动程序的16位应用程序 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c919ed8c3f3791720d67ebdcbf5cfbdbea2a0455
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307628"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>配合使用 16 位应用程序和 32 位驱动程序
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 请改用32位或64位驱动程序管理器。  
  
 您可以在基于 Windows 的系统上运行具有32位驱动程序的16位应用程序，前提是32位驱动程序没有显式调用创建线程 Win32 API 函数。 Windows on Windows （WOW）子系统在16位模式下运行应用程序，并将16位调用解析为操作系统。 ODBC thunk Dll 可将应用程序中的16位调用解析为32位驱动程序。 16位应用程序使用 Windows API，32位驱动程序使用 Win32 API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了16位应用程序如何与32位驱动程序通信。 16位驱动程序管理器和32位驱动程序之间是通用的 thunk Dll，它们将16位 ODBC 调用转换为32位 ODBC 调用。  
  
 ![16个&#45;位应用与 32&#45;位驱动程序的通信方式](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  每当16位应用程序与32位驱动程序交互时，32位驱动程序管理器始终将 "2.0" 作为该驱动程序支持的 ODBC 版本返回。  
  
## <a name="administration"></a>管理  
 您可以使用 ODBC 数据源管理器管理32位驱动程序的数据源。 若要在运行 Microsoft® Windows®2000的计算机上打开 "ODBC 管理器"，请打开 Windows "控制面板"，双击 "**管理工具**"，然后双击 "**数据源（ODBC）**"。 在运行早期版本的 Microsoft Windows 的计算机上，该图标名为**32 位 ODBC**或只是**ODBC**。  
  
 下图显示了16位应用程序如何调用32位驱动程序安装 DLL。 在16位安装程序 DLL 和32位驱动程序安装 DLL 之间，是一个将16位安装程序 DLL 调用转换为32位安装程序 DLL 调用的泛型 thunk DLL。  
  
 ![16个&#45;位应用调用 32&#45;位驱动程序安装 DLL 的方式](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 windows 上的 Windows （16位到32位 thunk）中，另一个名为 Ds32gt 的 thunk DLL 将通过32位安装程序 DLL 传递的16位参数值转换回16位。  
  
## <a name="components"></a>组件  
 MDAC 2.8 SP1 SDK 的 ODBC 组件包含以下文件，用于运行带有32位驱动程序的16位应用程序。 这些组件位于 \Redist 目录中。  
  
|文件名|说明|  
|---------------|-----------------|  
|Odbc16gt|16位 ODBC generic thunk DLL|  
|Odbc32gt|32位 ODBC generic thunk DLL|  
|Odbccp32|32位安装程序 DLL|  
|Odbcad32.exe|32位管理员程序|  
|Odbcinst.ini|安装程序帮助文件|  
|Ds16gt|16位驱动程序安装通用 thunk DLL|  
|Ctl3d32|32位三维窗口样式库|  
  
 此外，还需要以下与16位 ODBC 2.10 驱动程序管理器一起提供的文件，这些文件不属于 ODBC 3.51，并且应与16位应用程序一起安装。  
  
|文件名|说明|  
|---------------|-----------------|  
|Odbc .dll|16位驱动程序管理器|  
|Odbcinst.ini|16位安装程序 DLL|  
|Odbcadm|16位 ODBC 管理程序|
