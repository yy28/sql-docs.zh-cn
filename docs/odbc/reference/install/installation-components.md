---
title: 安装组件 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285247"
---
# <a name="installation-components"></a>安装组件
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 当用户运行安装程序时，安装过程将启动。 安装程序与*安装程序 DLL*和每个*驱动程序的驱动程序设置 DLL*结合使用。 安装程序和安装程序 DLL 都使用**SQLInstallDriverEx**和**SQLInstallTranslatorEx**函数中的参数来确定要为每个组件复制或删除哪些文件。 下图显示了这些安装组件之间的关系。  
  
 ![安装组件之间的关系](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  ODBC.inf 文件在 ODBC *2.x*中用于描述每个 ODBC 组件所需的文件，在 ODBC *3.x*中不使用。 提供 ODBC *3.x*组件的驱动程序不需要创建 Odbc.inf 文件。 **SQLInstallDriver**和**SQLInstallODBC**的删除，以及**SQLInstall 转换器**的弃用，使得 Odbc.inf 变得没有必要。 以前位于 Odbc.inf 的驱动程序关键字部分中的驱动程序信息现在在**SQLInstallDriverEx**中的*lpszDriver*参数中提供。 以前位于 Odbc.inf 的 [ODBC 转换器] 和翻译器规范部分的转换器信息现在在**SQLinstall 翻译器Ex**的*lpsz 转换器*参数中提供。 这些更改使 ODBC 安装程序在跨平台中更加便携。  
  
 有关这些组件的详细信息，请参阅本节末尾的以下主题。  
  
-   [安装程序](../../../odbc/reference/install/setup-program.md)  
  
-   [安装程序 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驱动程序安装程序 DLL](../../../odbc/reference/install/driver-setup-dll.md)
