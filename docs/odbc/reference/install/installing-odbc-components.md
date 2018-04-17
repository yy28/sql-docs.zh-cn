---
title: 安装 ODBC 组件 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 010922f0f92b1e4f49df5f44340d30404289bdc3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="installing-odbc-components"></a>安装 ODBC 组件
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，在 Windows 操作系统中包含 ODBC。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 本部分介绍如何安装和删除 ODBC 组件。 驱动程序开发人员始终安装的 ODBC 组件 （其驱动程序），因为它们需要阅读本节。 应用程序开发人员需要阅读此部分，仅当它们将提供的应用程序的 ODBC 组件。 ODBC 组件包括驱动程序管理器、 驱动程序、 转换器、 安装程序 DLL、 的是光标库，和相关的任何文件。 对于本部分，ODBC 应用程序不视为可 ODBC 组件。  
  
> [!NOTE]  
>  本节是特定于 Microsoft Windows 平台。 ODBC 组件在其他平台上的安装方式是特定于平台的。  
  
 ODBC 组件安装和删除基于组件的组件，不是文件的文件为基础。 例如，如果转换器包含转换器本身以及大量的数据文件，安装这些文件，删除作为一个组;它们必须不安装和删除基于文件的文件。 这是为了确保系统上存在唯一一个完整的组件。  
  
 有关安装和删除组件的目的，以下定义为在 ODBC 组件：  
  
-   **核心组件。** 驱动程序管理器、 光标库、 安装程序 DLL，和任何其他相关文件组成的核心组件和必须安装并作为一个组中删除。  
  
-   **驱动程序。** 每个驱动程序是一个单独的组件。  
  
-   **转换器。** 每个翻译人员是一个单独的组件。  
  
 使用 Unicode ODBC 3.5 及更高版本的支持，必须对使用 ODBC 的 OLE DB 组件给予某些考虑。 适用于 ODBC 的 OLE DB 访问接口的 1.1 版都写入到 ODBC 3.0 中的特定 Unicode 规范。 由于在 ODBC 3.5 中更改这些规范，它是所需版本 1.5 或更高版本的提供程序时使用 ODBC 3.5 及更高版本。 本部分包含以下主题。  
  
-   [安装组件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用情况计数](../../../odbc/reference/install/usage-counting.md)
