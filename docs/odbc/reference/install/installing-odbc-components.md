---
description: 安装 ODBC 组件
title: 安装 ODBC 组件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0250cc51b76cbda9c1091ebe1d696c2e569c037f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499743"
---
# <a name="installing-odbc-components"></a>安装 ODBC 组件
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 本部分介绍如何安装和删除 ODBC 组件。 由于驱动程序开发人员始终将 ODBC 组件安装 (其驱动程序) ，因此需要阅读本部分。 仅当应用程序开发人员将 ODBC 组件随应用程序一起发布时，它才需要读取此部分。 ODBC 组件包括驱动程序管理器、驱动程序、转换器、安装程序 DLL、游标库和所有相关文件。 出于本部分的目的，ODBC 应用程序不会被视为 ODBC 组件。  
  
> [!NOTE]  
>  本部分特定于 Microsoft Windows 平台。 ODBC 组件在其他平台上的安装方式是特定于平台的。  
  
 ODBC 组件按组件单独安装和删除，而不是逐个文件进行安装和删除。 例如，如果转换器由转换器本身和多个数据文件组成，则会以组的形式安装和删除这些文件;不能逐文件安装和删除这些文件。 这样做的原因是为了确保系统上只有完整的组件。  
  
 出于安装和删除组件的目的，以下内容定义为 ODBC 组件：  
  
-   **核心组件。** 驱动程序管理器、游标库、安装程序 DLL 和任何其他相关文件构成核心组件，并且必须作为一个组进行安装和删除。  
  
-   **因素.** 每个驱动程序都是单独的组件。  
  
-   **人员.** 每个转换器都是单独的组件。  
  
 由于 ODBC 3.5 和更高版本中支持 Unicode，因此必须考虑将 OLE DB 组件与 ODBC 一起使用。 适用于 ODBC 的 OLE DB 提供程序1.1 版本已写入 ODBC 3.0 中的特定 Unicode 规范。 由于这些规范在 ODBC 3.5 中发生了更改，因此，在使用 ODBC 3.5 和更高版本时，必须拥有版本1.5 或更高版本的提供程序。 本部分包含以下主题。  
  
-   [安装组件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用情况计数](../../../odbc/reference/install/usage-counting.md)
