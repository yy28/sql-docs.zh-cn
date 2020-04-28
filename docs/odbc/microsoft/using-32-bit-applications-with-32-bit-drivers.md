---
title: 将32位应用程序与32位驱动程序配合使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31512f9339b9d46225bb4f1198cb617a48509acb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307598"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>配合使用 32 位应用程序和 32 位驱动程序
可以运行包含32位驱动程序的32位应用程序。 32位应用程序和32位驱动程序使用 Win32® API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了32位应用程序与32位驱动程序的通信方式。 该应用程序将调用32位驱动程序管理器，该管理器又调用32位驱动程序。  
  
 ![32&#45;位应用与 32&#45;位驱动程序的通信方式](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  不要在 WindowsNT/Windows2000 上使用32位 thunk 安装程序 DLL。 尽管它与32位安装程序 DLL 具有相同的文件名，但它是不同的 DLL。  
  
## <a name="administration"></a>管理  
 您可以使用 ODBC 数据源管理器管理32位驱动程序的数据源。 若要在运行 Windows 2000 的计算机上打开 ODBC 管理员，请打开 Windows "控制面板"，双击 "**管理工具**"，然后双击 "**数据源（ODBC）**"。 在运行早期版本的 Microsoft Windows 的计算机上，该图标名为**32 位 ODBC**或只是**ODBC**。  
  
## <a name="components"></a>组件  
 ODBC 组件包含以下文件，用于运行包含32位驱动程序的32位应用程序。 这些组件位于 \Redist 目录中。  
  
|文件名|说明|  
|---------------|-----------------|  
|Odbc32.lib|32位驱动程序管理器|  
|Odbccp32|32位安装程序 DLL|  
|Odbcad32.exe|32位 ODBC 管理器程序|  
|Odbcinst.ini|安装程序帮助文件|  
|Msvcrt40.dll|C 运行时库|
