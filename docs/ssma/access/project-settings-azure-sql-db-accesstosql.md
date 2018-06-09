---
title: 项目设置 (Azure SQL DB) (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9d1666bf70cb07e616995dbd8f14fe4522cadc99
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774113"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>项目设置 (Azure SQL DB) (AccessToSQL)
SQL Azure 项目设置允许你配置要添加在连接对话框，并还允许在 SQL Azure 连接中实现检测信号机制的 SQL Azure 数据库后缀。  
  
SQL Azure 窗格位于**项目设置**和**默认项目设置**对话框。  
  
-   使用项目设置对话框中设置为当前项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单上，选择**项目设置**，单击**常规**底部的左窗格中，，然后选择**SQL Azure**。  
  
-   使用默认项目设置对话框中设置的所有项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单上，选择**DefaultProject 设置**，选择项目类型作为"SQL Azure"中**迁移目标版本**组合框，以访问 SQL Azure 窗格的设置中单击**常规**底部的左窗格中，，然后选择**SQL Azure**。  
  
## <a name="options"></a>“常规”  
  
## <a name="connectivity"></a>连接  
**检测信号间隔**  
  
指定要用于检测信号机制使 SQL Azure 连接中保持活动状态的时间间隔分钟： 秒的格式。  
  
**默认值**:"4:45  
  
应指定的值中正在： ss 的格式 (例如，"4:45 '或' 0:50 ')。  
  
**SQL Azure 服务器后缀**  
  
指定的 SQL Azure 服务器后缀  
  
**默认值**: database.windows.net。  
  
