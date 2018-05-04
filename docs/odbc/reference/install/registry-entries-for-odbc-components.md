---
title: ODBC 组件的注册表条目 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4cf61535ecda3e95f25dbd9e1b01a1d3ad25d4ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-for-odbc-components"></a>ODBC 组件的注册表项
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，在 Windows 操作系统中包含 ODBC。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 安装程序 DLL 会维护有关每个已安装的 ODBC 组件注册表中的信息。 在计算机上运行 Microsoft Windows NT 和 Microsoft Windows 95/98，此信息存储在注册表中的以下项下的子项：  
  
 HKEY_LOCAL_MACHINE  
  
 软件  
  
 ODBC  
  
 Odbcinst.ini  
  
 由于 Odbcinst.ini 是 HKEY_LOCAL_MACHINE 树的子项，ODBC 组件有关的信息可供计算机的所有用户。  
  
 本部分包含以下主题。  
  
-   [ODBC 核心子项](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [ODBC 驱动程序子项](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [驱动程序规范子项](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [默认驱动程序子项](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [ODBC 转换器子项](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [转换器规范子项](../../../odbc/reference/install/translator-specification-subkeys.md)
