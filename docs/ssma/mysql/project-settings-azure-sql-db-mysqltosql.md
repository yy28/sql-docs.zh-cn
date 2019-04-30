---
title: 项目设置 (Azure SQL DB) (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e0c16fe617b5808f22f15cdf89af8dc7a1e79898
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311986"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>项目设置 (Azure SQL DB) (MySQLToSQL)
SQL Azure 项目设置可配置要在连接对话框中添加并允许在 SQL Azure 连接实施检测信号机制的 SQL Azure 数据库后缀。  
  
SQL Azure 窗格现已推出**项目设置**并**默认项目设置**对话框。  
  
-   使用项目设置对话框中设置当前项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单中，选择**项目设置**，单击**常规**在左窗格中，并选择底部**SQLAzure**。  
  
-   使用默认项目设置对话框中设置的所有项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单中，选择**DefaultProject 设置**，选择作为从 SQL Azure 迁移项目类型**迁移目标版本**删除设置 SQL Azure 在窗格中，单击下访问**常规**在左窗格中，并选择底部**SQL Azure**。  
  
## <a name="options"></a>选项  
  
## <a name="connectivity"></a>连接  
**检测信号间隔**  
  
指定要用于检测信号机制，以便在保持 SQL Azure 连接时间间隔分钟： 秒的格式。  
  
**默认值**:"4:45  
  
应指定的值中是： ss 的格式 (例如，"4:45 或"0:50)。  
  
**SQL Azure Server Suffix**  
  
指定 SQL Azure 服务器后缀  
  
**默认值**: database.windows.net。  
  
