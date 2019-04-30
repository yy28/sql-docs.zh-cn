---
title: 使用 32 位应用程序和 32 位驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4f0b21bba9e56cad076ae08f5a561cc972d2ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213464"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>配合使用 32 位应用程序和 32 位驱动程序
可以使用 32 位驱动程序运行 32 位应用程序。 32 位应用程序和 32 位驱动程序使用 Win32® API。  
  
## <a name="architecture"></a>体系结构  
 下图显示了 32 位应用程序与 32 位驱动程序进行通信。 在应用程序调用 32 位驱动程序管理器，后者又调用 32 位驱动程序。  
  
 ![如何 32&#45;具有 32 位应用程序的通信&#45;位驱动程序](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  不要在 windows Nt/windows 2000 上使用 32 位形式转换安装程序 DLL。 尽管它具有与 32 位安装程序 DLL 文件同名，但它是一个不同的 DLL。  
  
## <a name="administration"></a>管理  
 可以通过使用 ODBC 数据源管理器管理 32 位驱动程序的数据的源。 若要打开 ODBC 管理器中运行 Windows 2000 的计算机上，打开 Windows 控制面板中，双击**管理工具**，然后双击**数据源 (ODBC)**。 在计算机上运行的 Microsoft Windows 的早期版本，名为图标**32 位 ODBC**或只需**ODBC**。  
  
## <a name="components"></a>组件  
 ODBC 组件包括以下文件为运行 32 位驱动程序使用 32 位应用程序。 这些组件是 \Redist 目录中。  
  
|File name|描述|  
|---------------|-----------------|  
|Odbc32.dll|32 位驱动程序管理器|  
|Odbccp32.dll|32 位安装程序 DLL|  
|Odbcad32.exe|32 位 ODBC 管理器程序|  
|Odbcinst.hlp|安装程序帮助文件|  
|Msvcrt40.dll|C 运行时库|
