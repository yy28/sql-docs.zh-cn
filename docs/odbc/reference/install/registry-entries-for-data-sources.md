---
title: 数据源的注册表项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fe76ba3926f2883e2518e255eddf0d567134f4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "70009357"
---
# <a name="registry-entries-for-data-sources"></a>数据源的注册表项
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 安装程序 DLL 会在注册表中维护有关每个数据源的信息。 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 中，此信息存储在注册表中以下两个密钥之一下的子项中：  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 使用哪种密钥取决于数据源是否为*系统数据源（* 对所有用户都可用）或*用户数据源（* 仅适用于当前用户）。 系统数据源存储在 HKEY_LOCAL_MACHINE 树上，用户数据源存储在 HKEY_CURRENT_USER 树中。 在所有其他方面，系统数据源和用户数据源相同。  
  
 本部分包含下列主题。  
  
-   [ODBC 数据源子项](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [默认子项](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 子项](../../../odbc/reference/install/odbc-subkey.md)
