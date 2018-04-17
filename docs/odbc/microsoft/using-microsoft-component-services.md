---
title: 使用 Microsoft 组件服务 |Microsoft 文档
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
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 99ef6529d40d626a5f7c2bab97120f4173c8d5d7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft 组件服务
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 你可以在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 上启用 Oracle 数据库用于事务性组件服务 （或 MTS，如果你使用的 Windows NT）。 若要启用 Oracle 数据库以便使用支持事务的组件服务，系统管理员应创建一个名为 V$ XATRANS$ 的视图。 若要创建此脚本，必须运行 Oracle 提供的脚本。 有关详细信息，请参阅的组件服务帮助或 Oracle 文档。
