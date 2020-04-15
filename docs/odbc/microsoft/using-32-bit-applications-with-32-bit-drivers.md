---
title: 使用 32 位应用程序与 32 位驱动程序 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307598"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>配合使用 32 位应用程序和 32 位驱动程序
您可以使用 32 位驱动程序运行 32 位应用程序。 32 位应用程序和 32 位驱动程序使用 Win32® API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了 32 位应用程序如何与 32 位驱动程序进行通信。 该应用程序调用 32 位驱动程序管理器，该管理器又调用 32 位驱动程序。  
  
 ![32 个&#45;位应用如何与 32 个&#45;位驱动程序进行通信](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  请勿在 WindowsNT/Windows2000 上使用 32 位分叉安装程序 DLL。 尽管它与 32 位安装程序 DLL 具有相同的文件名，但它是不同的 DLL。  
  
## <a name="administration"></a>管理  
 您可以使用 ODBC 数据源管理员管理 32 位驱动程序的数据源。 要在运行 Windows 2000 的计算机上打开 ODBC 管理员，请打开 Windows 控制面板，双击**管理工具**，然后双击**数据源 （ODBC）。** 在运行微软早期版本的 Windows 的计算机上，该图标被命名为**32 位 ODBC**或简称**ODBC**。  
  
## <a name="components"></a>组件  
 ODBC 组件包括以下文件，用于使用 32 位驱动程序运行 32 位应用程序。 这些组件位于 @Redist 目录中。  
  
|文件名|描述|  
|---------------|-----------------|  
|奥德bc32.dll|32 位驱动程序管理器|  
|奥德班德32.dll|32 位安装程序 DLL|  
|奥德布卡德32.exe|32 位 ODBC 管理员程序|  
|奥德布金斯特.hlp|安装程序帮助文件|  
|Msvcrt40.dll|C 运行时库|
