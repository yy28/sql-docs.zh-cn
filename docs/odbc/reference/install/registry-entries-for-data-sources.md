---
title: 数据源的注册表条目 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c225109657906459d86ab5d19e441158c16ca57d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-for-data-sources"></a>数据源的注册表项
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，在 Windows 操作系统中包含 ODBC。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 安装程序 DLL 维护注册表中有关每个数据源的信息。 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98，此信息存储在注册表中的以下两个密钥之一下的子项：  
  
 HKEY_LOCAL_MACHINE  
  
 软件  
  
 ODBC  
  
 Odbc.ini  
  
 HKEY_CURRENT_USER  
  
 软件  
  
 ODBC  
  
 Odbc.ini  
  
 使用哪些密钥取决于数据源是*系统数据源，*这是可供所有用户，或*用户数据源，*这是仅供当前用户。 在 HKEY_LOCAL_MACHINE 树中，存储系统数据源和用户数据源将存储在 HKEY_CURRENT_USER 树。 在所有其他方面，系统数据源和用户数据源均相同。  
  
 本部分包含以下主题。  
  
-   [ODBC 数据源子项](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [默认子项](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 子项](../../../odbc/reference/install/odbc-subkey.md)
