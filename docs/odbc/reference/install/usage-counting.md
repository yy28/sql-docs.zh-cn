---
title: 使用情况计数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca2a52eb08cdf1b1b9cb5a23805da34aab915b7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273390"
---
# <a name="usage-counting"></a>使用情况计数
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包括在 Windows 操作系统中。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 每个组件在注册表中维护两种类型的使用计数： 组件使用情况计数和一个或多个可选文件使用情况计数。 组件使用情况计数可帮助安装程序 DLL 维护注册表项。 它存储在 ODBC 核心、 驱动程序和转换器子项下的 UsageCount 值。 有关 UsageCount 值和有关这些子项的详细信息的格式，请参阅[ODBC 组件的注册表项](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 首次安装一个组件，安装程序就会为其创建一个子项 DLL 并设置为 1 的子项中 UsageCount 值的数据。 重新安装该组件时，安装程序 DLL 递增的使用计数。 删除该组件后，安装程序 DLL 减少使用情况计数着。 如果使用情况计数降为 0，安装程序 DLL 将删除该组件的子项。  
  
> [!CAUTION]  
>  应用程序不应以物理方式删除驱动程序管理器文件时的组件使用计数和文件使用情况计数归零。  
  
 文件使用情况计数帮助确定何时文件必须实际进行复制或删除而不是递增或递减的使用计数。 这非常重要，因为 ODBC 组件，因此 ODBC 组件中的文件共享，可安装或删除的各种应用程序。 如果组件使用情况计数和文件使用情况计数归零，该应用程序可以删除驱动程序和翻译文件。 驱动程序管理器文件但是不应，被删除时的组件使用计数和文件使用率计数已达到零，因为这些文件可以由其他应用程序具有不会增加文件使用情况计数。  
  
> [!NOTE]  
>  文件使用情况计数是 Microsoft® WindowsNT®/Windows2000 中可选的。  
  
 文件使用情况计数由安装程序后，它调用维护**SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLInstallTranslatorEx**， **SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator**。  
  
 首次安装一个组件，安装程序或安装程序 DLL 创建一个值为每个文件位于下列键中已不在系统的组件：  
  
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
>  SharedDlls  
  
 它将这些值的数据设置为 1，并将文件复制到系统。 重新安装该组件时，安装程序或安装程序 DLL 会递增的使用情况计数。 删除该组件后，安装程序或安装程序 DLL 递减的使用计数。 如果任何使用情况计数降为 0，安装程序或安装程序 DLL 中删除文件的值并，如果该组件是一个驱动程序或翻译，删除文件。 不应删除驱动程序管理器文件。  
  
 下表中显示文件使用情况计数值的格式。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|*full-path*|REG_DWORD|*计数*|  
  
 例如，假设 Informix 的驱动程序使用 Infrmx32.dll 和 Infrmx32.hlp 文件，并假设此驱动程序已安装程序两次。 Informix 驱动程序的需要在 SharedDlls 子项下的值将按如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
