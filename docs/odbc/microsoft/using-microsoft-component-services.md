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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb5763058fa198cbad7464434e31942ef8d6cd7d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307578"
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft 组件服务
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 上，你可以启用 Oracle 数据库来处理事务组件服务（如果使用的是 Windows NT，则为 MTS）。 若要允许 Oracle 数据库使用支持事务的组件服务，系统管理员应创建名为 V $ XATRANS $ 的视图。 若要创建此脚本，必须运行 Oracle 提供的脚本。 有关详细信息，请参阅组件服务帮助或 Oracle 文档。
