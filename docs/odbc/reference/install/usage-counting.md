---
title: 使用情况计数 |Microsoft 文档
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
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd0d07195dfb0f3ece3cc6f574b5cc1544cf8104
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="usage-counting"></a>使用情况计数
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，在 Windows 操作系统中包含 ODBC。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 在每个组件的注册表中维护两种类型的使用计数： 一个组件使用计数和一个或多个可选文件使用情况计数。 组件使用率计数可帮助安装程序 DLL 维护注册表项。 它存储在 ODBC 核心、 驱动程序，以及转换器子项下的 UsageCount 值。 UsageCount 值以及有关这些子项的详细信息的格式，请参阅[ODBC 组件的注册表项](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 在首次安装组件，安装程序就为其创建一个子项 DLL 并在 1 到该子项设置 UsageCount 值的数据。 当再次安装的组件时，安装程序 DLL 递增的使用计数。 在删除该组件后，安装程序 DLL 递减使用情况进行计数。 如果使用率计数降为 0，安装程序 DLL 中删除组件的子项。  
  
> [!CAUTION]  
>  应用程序不应以物理方式删除驱动程序管理器文件的组件使用计数和文件使用情况计数达到零时。  
  
 文件使用情况计数帮助确定当文件必须实际为复制或删除而不是递增或递减的使用计数。 这非常重要，因为 ODBC 组件，因此 ODBC 组件中的文件共享和可以要安装或删除通过各种应用程序。 如果组件使用率计数和文件使用情况计数归零，则应用程序可以删除驱动程序和转换器文件。 驱动程序管理器文件应不是，但是，删除时的组件使用计数和文件使用率计数已达到零，因为这些文件可以由其他应用程序具有不会增加文件使用率计数。  
  
> [!NOTE]  
>  文件使用情况计数是在 Microsoft® WindowsNT®/windows2000 本机可选的。  
  
 文件使用情况计数由安装程序后它会调用维护**SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLInstallTranslatorEx**， **SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator**。  
  
 首次安装组件，安装程序或安装程序 DLL 创建值为每个文件在以下注册表项中已不在系统的该组件：  
  
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
>  需要在 SharedDlls  
  
 它将这些值的数据设置为 1，并将文件复制到系统。 当再次安装的组件时，安装程序或安装程序 DLL 将递增的使用情况计数。 在删除该组件后，安装程序或安装程序 DLL 递减的使用计数。 如果任何使用率计数降为 0，安装程序或安装程序 DLL 中删除文件的值并且，如果组件是驱动程序或一个转换器，删除文件。 不应删除驱动程序管理器文件。  
  
 下表中显示文件使用情况计数值的格式。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|*完整路径*|REG_DWORD|*计数*|  
  
 例如，假设 Informix 的驱动程序使用 Infrmx32.dll 和 Infrmx32.hlp 文件，并假设此驱动程序已安装程序两次。 Informix 驱动程序的需要在 SharedDlls 子项下的值将如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
