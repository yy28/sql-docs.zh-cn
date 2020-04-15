---
title: 安装 ODBC 组件 |微软文档
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
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298977"
---
# <a name="installing-odbc-components"></a>安装 ODBC 组件
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 本节介绍如何安装和删除 ODBC 组件。 由于驱动程序开发人员始终安装 ODBC 组件（其驱动程序），因此他们需要阅读此部分。 应用程序开发人员只有在将 ODBC 组件随其应用程序一起提供时，才需要阅读本节。 ODBC 组件包括驱动程序管理器、驱动程序、翻译人员、安装程序 DLL、游标库和任何相关文件。 就本节而言，ODBC 应用程序不被视为 ODBC 组件。  
  
> [!NOTE]  
>  本节特定于 Microsoft Windows 平台。 如何在其他平台上安装 ODBC 组件是特定于平台的。  
  
 ODBC 组件是逐个组件安装和删除的，而不是逐个文件的。 例如，如果译员本身和多个数据文件组成，这些文件将作为一个组进行安装和删除;不得逐个文件安装和删除它们。 这样做的原因是为了确保系统上仅存在完整的组件。  
  
 为了安装和拆卸组件，以下定义为 ODBC 组件：  
  
-   **核心组件。** 驱动程序管理器、游标库、安装程序 DLL 和任何其他相关文件组成核心组件，必须作为一个组进行安装和删除。  
  
-   **司机。** 每个驱动程序都是单独的组件。  
  
-   **翻译。** 每个转换器都是一个单独的组件。  
  
 在 ODBC 3.5 及更高版本中 Unicode 的支持下，必须考虑将 OLE DB 组件与 ODBC 一起使用。 ODBC 的 OLE DB 提供程序的 1.1 版本写入了 ODBC 3.0 中的特定 Unicode 规范。 由于这些规范在 ODBC 3.5 中发生了变化，因此在使用 ODBC 3.5 及更高版本时，有必要拥有提供程序的版本 1.5 或更高版本。 本部分包含以下主题。  
  
-   [安装组件](../../../odbc/reference/install/installation-components.md)  
  
-   [使用情况计数](../../../odbc/reference/install/usage-counting.md)
