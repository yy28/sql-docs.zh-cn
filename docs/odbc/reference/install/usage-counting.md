---
title: 使用情况计数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296017"
---
# <a name="usage-counting"></a>使用情况计数
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 每个组件的注册表中维护两种类型的使用计数：组件使用计数和一个或多个可选文件使用情况计数。 组件使用计数可帮助安装程序 DLL 维护注册表项。 它存储在 ODBC 核心、驱动程序和转换器子键下的"使用情况计数"值中。 有关使用计数值的格式以及有关这些子键的详细信息，请参阅[ODBC 组件的注册表项](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 首次安装组件时，安装程序 DLL 会为其创建一个子键，并将该子键中的"使用情况计数"值的数据集到 1。 再次安装组件时，安装程序 DLL 会增加使用计数。 删除组件后，安装程序 DLL 会减少使用计数。 如果使用计数降至 0，安装程序 DLL 将删除组件的子键。  
  
> [!CAUTION]  
>  当组件使用计数和文件使用计数达到零时，应用程序不应物理删除驱动程序管理器文件。  
  
 文件使用情况计数有助于确定何时必须实际复制或删除文件，而不是增加或删除使用计数。 这一点很重要，因为 ODBC 组件以及 ODBC 组件中的文件是共享的，并且可以由各种应用程序安装或删除。 如果组件使用计数和文件使用计数达到零，应用程序可以删除驱动程序和转换器文件。 但是，当组件使用计数和文件使用计数都达到零时，不应删除驱动程序管理器文件，因为这些文件可以由未增加文件使用计数的其他应用程序使用。  
  
> [!NOTE]  
>  文件使用情况计数在 Microsoft 中是可选的® WindowsNT ®/Windows2000。  
  
 文件使用情况计数由安装程序在调用**SQLInstall 驱动程序管理器****、SQLInstallDriverEx、SQLinstall****翻译器****、SQLRemove驱动程序管理器****、SQL删除驱动程序**或**SQLRemove 转换器**后进行维护。  
  
 首次安装组件时，安装程序或安装程序 DLL 会为该组件中尚未在系统上的每个文件在以下键下创建一个值：  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  软件  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  共享 Dlls  
  
 它将这些值的数据设置为 1，并将文件复制到系统。 再次安装组件时，安装程序或安装程序 DLL 会增加使用量计数。 删除组件后，安装程序或安装程序 DLL 会减少使用量。 如果任何使用计数降至 0，安装程序或安装程序 DLL 将删除文件的值，如果组件是驱动程序或转换器，则删除该文件。 不应删除驱动程序管理器文件。  
  
 下表显示了文件使用情况计数值的格式。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|*全路径*|REG_DWORD|*count*|  
  
 例如，假设 Informix 的驱动程序使用 Infrmx32.dll 和 Infrmx32.hlp 文件，并假设此驱动程序已安装两次。 Informix 驱动程序的"共享Dll"子键下的值如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
