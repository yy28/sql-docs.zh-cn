---
title: 使用 16 位和 32 位应用程序，使用 32 位驱动程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce996a7c4816d4d14491e226f891904b6cf8c02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307608"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>配合使用 16 位和 32 位应用程序与 32 位驱动程序
> [!IMPORTANT]  
>  16 位应用程序支持将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 开发 32 位或 64 位应用程序。  
  
 使用 ODBC 数据访问组件，您可以使用具有 32 位驱动程序的 16 位和 32 位应用程序。 微软® Windows ® 95/98 和微软 Windows NT®/Windows 2000 操作系统支持以下应用程序和驱动程序的组合：  
  
-   具有 32 位驱动程序的 16 位应用程序  
  
-   32 位应用程序，具有 32 位驱动程序  
  
 不支持使用具有 16 位驱动程序的 32 位应用程序。  
  
> [!NOTE]  
>  从 ODBC 版本 3.0 的发布开始，Windows NT 4.0 一直支持。  
  
 ODBC 包括支持上述配置所需的 ODBC 组件，通过"访问"动态链接库 （DLL） 将 16 位地址转换为 32 位地址，反之亦然。 安装程序确定您正在使用哪个操作系统并安装该系统所需的 ODBC 组件。 您还可以选择安装所有系统使用的 ODBC 组件。  
  
 在大多数情况下，将应用程序或驱动程序从 16 位移植到 32 位涉及五种类型的更改：  
  
-   对消息处理代码的更改  
  
-   更改，因为整数和句柄为 32 位  
  
-   对 Windows 应用程序编程接口 （API） 的调用中的更改  
  
-   更改以使驱动程序线程安全  
  
-   对 ODBC 组件的更改  
  
 从应用程序或驱动程序编程的角度来看，16 位和 32 位 ODBC 组件之间的主要区别是它们具有不同的文件名。 从系统的角度来看，每个应用程序或驱动程序连接的体系结构是不同的，用于管理数据源的工具也不同。  
  
 本部分包含以下主题。  
  
-   [配合使用 16 位应用程序和 32 位驱动程序](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [配合使用 32 位应用程序和 32 位驱动程序](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
