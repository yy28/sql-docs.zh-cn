---
description: 使用 Microsoft 组件服务
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
ms.openlocfilehash: 8214b706394c9fe8e2b8a6fd2491156292475fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471339"
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft 组件服务
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 如果使用的是 Windows NT) 在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 上，则可以使 Oracle 数据库能够与事务组件服务 (或 MTS 一起使用。 若要允许 Oracle 数据库使用支持事务的组件服务，系统管理员应创建名为 V $ XATRANS $ 的视图。 若要创建此脚本，必须运行 Oracle 提供的脚本。 有关详细信息，请参阅组件服务帮助或 Oracle 文档。
