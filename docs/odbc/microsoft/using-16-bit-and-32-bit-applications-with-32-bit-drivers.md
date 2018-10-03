---
title: 使用 16 位和 32 位应用程序和 32 位驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8540983b84d4d39fe5a02b92a1e3a3606350d36d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714445"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>配合使用 16 位和 32 位应用程序与 32 位驱动程序
> [!IMPORTANT]  
>  16 位应用程序支持将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是开发 32 位或 64 位应用程序。  
  
 使用 ODBC 数据访问组件，可以使用 16 位和 32 位应用程序与 32 位驱动程序。 Microsoft® Windows® 95/98 和 Microsoft Windows/Windows 2000 操作系统支持应用程序和驱动程序的以下的组合：  
  
-   16 位应用程序与 32 位驱动程序  
  
-   32 位应用程序与 32 位驱动程序  
  
 不支持 32 位应用程序使用 16 位驱动程序。  
  
> [!NOTE]  
>  ODBC 版本 3.0 版本开始，已支持 Windows NT 4.0。  
  
 ODBC 包括支持通过"形式转换"动态链接库 (Dll) 来将 16 位地址转换为 32 位地址，反之亦然，上面的配置所需的 ODBC 组件。 安装程序将确定使用的，安装 ODBC 组件，该系统所需的操作系统。 您还可以选择安装所有系统都使用的 ODBC 组件。  
  
 在大多数情况下，移植应用程序或驱动程序从 16 位到 32 位涉及五种类型的更改：  
  
-   对消息处理代码的更改  
  
-   会更改，因为整数和句柄都是 32 位  
  
-   对 Windows 应用程序编程接口 (Api) 的调用中的更改  
  
-   若要使线程安全的驱动程序的更改  
  
-   对 ODBC 组件的更改  
  
 从应用程序或驱动程序编程的角度来看，16 位和 32 位 ODBC 组件之间的主要区别是它们具有不同的文件的名称。 从系统角度看，每个应用程序或驱动程序连接的体系结构不同，用来管理数据源的工具有不同。  
  
 本部分包含以下主题。  
  
-   [配合使用 16 位应用程序和 32 位驱动程序](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [配合使用 32 位应用程序和 32 位驱动程序](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
