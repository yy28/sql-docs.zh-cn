---
title: 使用 16 位应用程序与 32 位驱动程序 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307628"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>配合使用 16 位应用程序和 32 位驱动程序
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 改用 32 位或 64 位驱动程序管理器。  
  
 只要 32 位驱动程序不显式调用创建线程的 Win32 API 函数，就可以在基于 Windows 的系统上运行具有 32 位驱动程序的 16 位应用程序。 Windows 上的 Windows （WOW） 子系统以 16 位模式运行应用程序，并解决对操作系统的 16 位调用。 ODBC thund DLL 解析从应用程序到 32 位驱动程序的 16 位调用。 16 位应用程序使用 Windows API，32 位驱动程序使用 Win32 API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了 16 位应用程序如何与 32 位驱动程序进行通信。 在 16 位驱动程序管理器和 32 位驱动程序之间，是通用的 DUN，可将 16 位 ODBC 调用转换为 32 位 ODBC 调用。  
  
 ![16&#45;位应用如何与 32 个位驱动程序&#45;位驱动程序进行通信](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  每当 16 位应用程序与 32 位驱动程序交互时，32 位驱动程序管理器始终返回"2.0"作为驱动程序支持的 ODBC 版本。  
  
## <a name="administration"></a>管理  
 您可以使用 ODBC 数据源管理员管理 32 位驱动程序的数据源。 要在运行 Microsoft ® Windows 的计算机上打开 ODBC 管理员® 2000，请打开 Windows 控制面板，双击**管理工具**，然后双击**数据源 （ODBC）。** 在运行微软早期版本的 Windows 的计算机上，该图标被命名为**32 位 ODBC**或简称**ODBC**。  
  
 下图显示了 16 位应用程序如何调用 32 位驱动程序设置 DLL。 在 16 位安装程序 DLL 和 32 位驱动程序设置 DLL 之间，DLL 是一种通用的分接 DLL，可将 16 位安装程序 DLL 调用转换为 32 位安装程序 DLL 调用。  
  
 ![16&#45;位应用如何调用 32&#45;位驱动程序设置 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 在 Windows 上的 Windows（16 位到 32 位）中，另一个名为 Ds32gt.dll 的 dLL 将通过 32 位设置 DLL 传递的 16 位参数值转换回 16 位。  
  
## <a name="components"></a>组件  
 MDAC 2.8 SP1 SDK 的 ODBC 组件包括以下文件，用于运行具有 32 位驱动程序的 16 位应用程序。 这些组件位于 @Redist 目录中。  
  
|文件名|描述|  
|---------------|-----------------|  
|奥德bc16gt.dll|16 位 ODBC 通用分叉 DLL|  
|奥德bc32gt.dll|32 位 ODBC 通用分叉 DLL|  
|奥德班德32.dll|32 位安装程序 DLL|  
|奥德布卡德32.exe|32 位管理员程序|  
|奥德布金斯特.hlp|安装程序帮助文件|  
|Ds16gt.dll|16 位驱动程序设置通用分叉 DLL|  
|Ctl3d32.dll|32 位三维窗口样式库|  
  
 此外，以下文件以及 16 位 ODBC 2.10 驱动程序管理器（不属于 ODBC 3.51）是必需的，并且应该与 16 位应用程序一起安装。  
  
|文件名|描述|  
|---------------|-----------------|  
|奥德布布.dll|16 位驱动程序管理器|  
|奥德布金斯特.dll|16 位安装程序 DLL|  
|奥德布德姆.exe|16 位 ODBC 管理员程序|
