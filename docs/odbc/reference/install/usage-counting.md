---
title: 使用量计数 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296017"
---
# <a name="usage-counting"></a>使用情况计数
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 在注册表中，每个组件都保留两种类型的使用计数：组件使用计数和一个或多个可选的文件使用计数。 组件使用计数有助于安装程序 DLL 维护注册表项。 它存储在 ODBC Core、driver 和 translator 子项下的 UsageCount 值中。 有关 UsageCount 值的格式以及这些子项的详细信息，请参阅[ODBC 组件的注册表项](../../../odbc/reference/install/registry-entries-for-odbc-components.md)。  
  
 第一次安装组件时，安装程序 DLL 将为其创建一个子项，并将该子项中 UsageCount 值的数据设置为1。 再次安装该组件时，安装程序 DLL 会递增使用量计数。 删除该组件时，安装程序 DLL 将递减使用计数。 如果使用计数降到0，则安装程序 DLL 会删除组件的子项。  
  
> [!CAUTION]  
>  当组件使用计数和文件使用计数都为零时，应用程序不应物理删除驱动程序管理器文件。  
  
 文件使用计数可帮助确定文件的复制或删除时间，而不是递增或递减使用次数。 这一点很重要，因为 ODBC 组件（以及 ODBC 组件中的文件）是共享的，并且可由多种应用程序进行安装或删除。 如果组件使用计数和文件使用计数达到零，则应用程序可以删除驱动程序和转换器文件。 但是，当组件用量计数和文件使用计数都为零时，不应删除驱动程序管理器文件，这是因为这些文件可以由尚未增加文件使用计数的其他应用程序使用。  
  
> [!NOTE]  
>  文件使用计数在 Microsoft® WindowsNT®/Windows2000. 中是可选的  
  
 文件使用计数在调用**SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLInstallTranslatorEx**、 **SQLRemoveDriverManager**、 **SQLRemoveDriver**或**SQLRemoveTranslator**后由安装程序维护。  
  
 第一次安装组件时，安装程序或安装程序 DLL 会在该组件中不存在系统上的每个文件的下面创建一个值：  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  软件列表  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 它将这些值的数据设置为1，并将文件复制到系统。 再次安装该组件时，安装程序或安装程序 DLL 会递增使用量计数。 删除该组件时，安装程序或安装程序 DLL 将递减使用计数。 如果任何用量计数降到0，则安装程序或安装程序 DLL 会删除该文件的值，如果该组件是驱动程序或转换器，则会删除该文件。 不应删除驱动程序管理器文件。  
  
 下表显示了文件使用计数值的格式。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|*完整路径*|REG_DWORD|*计数*|  
  
 例如，假设 Informix 的驱动程序使用 Infrmx32 和 Infrmx32 文件，并且假设此驱动程序已安装了两次。 Informix 驱动程序的 SharedDlls 子项下的值如下所示：  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
