---
title: 安装组件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a196e9b935229fa03c6dd0eda92b8e99e69f0ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285247"
---
# <a name="installation-components"></a>安装组件
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 当用户运行安装程序时，将启动安装过程。 安装程序与*安装程序 dll*以及每个驱动程序的*驱动程序安装*程序 dll 一起工作。 安装程序和安装程序 DLL 均使用**SQLInstallDriverEx**和**SQLInstallTranslatorEx**函数中的参数来确定要为每个组件复制或删除的文件。 下图显示了这些安装组件之间的关系。  
  
 ![安装组件之间的关系](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Odbc 2.x 中使用的 Odbc. *x*用于说明每个 odbc 组件所需的文件并不*用于 odbc 2.x*。 提供 ODBC 1.x 组件的驱动程序无需*创建 odbc .inf*文件。 删除**SQLInstallDriver**和**SQLInstallODBC**以及弃用**SQLInstallTranslator**，这是不必要的。 现在，在**SQLInstallDriverEx**的*lpszDriver*参数中提供了在 Odbc 的 driver 关键字部分中使用的驱动程序信息。 现已在**SQLInstallTranslatorEx**的*lpszTranslator*参数中提供了用于在 Odbc 的 [Odbc 转换器] 和转换器规范部分中提供的转换器信息。 这些更改允许 ODBC 安装程序在平台之间更易于移植。  
  
 有关这些组件的详细信息，请参阅本节末尾的以下主题。  
  
-   [安装程序](../../../odbc/reference/install/setup-program.md)  
  
-   [安装程序 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驱动程序安装程序 DLL](../../../odbc/reference/install/driver-setup-dll.md)
