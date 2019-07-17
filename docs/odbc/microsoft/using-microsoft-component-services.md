---
title: 使用 Microsoft 组件服务 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91d6dcf0ca7f87d6ed510d582f7a7ba0f80e8c74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088149"
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft 组件服务
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 可以在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 启用要使用事务性组件服务 （或 MTS，如果您使用的 Windows NT） 的 Oracle 数据库。 若要启用的 Oracle 数据库，以便使用支持事务的组件服务，系统管理员应创建一个名为 V$ XATRANS$ 视图。 若要创建此脚本，必须运行 Oracle 提供的脚本。 有关详细信息，请参阅组件服务帮助或 Oracle 文档。
