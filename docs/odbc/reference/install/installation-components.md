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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34d1b6d143f6f40d73e2feeb0b718f3c3b3248fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094134"
---
# <a name="installation-components"></a>安装组件
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包括在 Windows 操作系统中。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 用户在运行安装程序时，安装过程开始。 安装程序结合工作*安装程序 DLL*和一个*驱动程序安装程序 DLL*每个驱动程序。 安装程序和安装程序 DLL 都使用中的自变量**SQLInstallDriverEx**并**SQLInstallTranslatorEx**函数来确定哪些文件复制或删除每个组件。 下图显示了这些安装组件之间的关系。  
  
 ![安装组件之间的关系](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  在 ODBC 中使用的 Odbc.inf 文件*2.x*来描述所需的每个 ODBC 文件组件中不使用 ODBC *3.x*。 附带 ODBC 驱动程序*3.x*组件不需要创建一个 Odbc.inf 文件。 删除**SQLInstallDriver**并**SQLInstallODBC**，并不推荐使用的**SQLInstallTranslator**，呈现 Odbc.inf 不必要。 中现在提供 Odbc.inf Driver 关键字部分中要使用的驱动程序信息*lpszDriver*中的参数**SQLInstallDriverEx**。 转换器信息的使用 [ODBC 转换器] 是和中现在提供转换器规范部分 Odbc.inf *lpszTranslator*的参数**SQLInstallTranslatorEx**。 这些更改允许 ODBC 安装程序可以跨平台可移植性。  
  
 有关这些组件的详细信息，请参阅本部分末尾的以下主题。  
  
-   [安装程序](../../../odbc/reference/install/setup-program.md)  
  
-   [安装程序 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驱动程序安装程序 DLL](../../../odbc/reference/install/driver-setup-dll.md)
