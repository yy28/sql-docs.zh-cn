---
title: 项目设置 (Azure SQL DB) (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2307a62c05503a231c3ee16b79efb25e964f55bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453466"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>项目设置 (Azure SQL DB) (AccessToSQL)
SQL Azure 项目设置可配置要在连接对话框中添加并允许在 SQL Azure 连接实施检测信号机制的 SQL Azure 数据库后缀。  
  
SQL Azure 窗格现已推出**项目设置**并**默认项目设置**对话框。  
  
-   使用项目设置对话框中设置当前项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单中，选择**项目设置**，单击**常规**在左窗格中，并选择底部**SQLAzure**。  
  
-   使用默认项目设置对话框中设置的所有项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单中，选择**DefaultProject 设置**，为"SQL Azure"中选择项目类型**迁移目标版本**到组合框访问 SQL Azure 窗格中的设置，请单击**常规**在左窗格中，并选择底部**SQL Azure**。  
  
## <a name="options"></a>选项  
  
## <a name="connectivity"></a>连接  
**检测信号间隔**  
  
指定要用于检测信号机制，以便在保持 SQL Azure 连接时间间隔分钟： 秒的格式。  
  
**默认值**:"4:45  
  
应指定的值中是： ss 的格式 (例如，"4:45 或"0:50)。  
  
**SQL Azure Server Suffix**  
  
指定 SQL Azure 服务器后缀  
  
**默认值**: database.windows.net。  
  
