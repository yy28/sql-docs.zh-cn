---
title: 项目设置 (Azure SQL DB) (MySQLToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46dfaa1f7b35f87d13fc3a88fb00d6a26a1cf27f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>项目设置 (Azure SQL DB) (MySQLToSQL)
SQL Azure 项目设置允许你配置要添加在连接对话框，并还允许在 SQL Azure 连接中实现检测信号机制的 SQL Azure 数据库后缀。  
  
SQL Azure 窗格位于**项目设置**和**默认项目设置**对话框。  
  
-   使用项目设置对话框中设置为当前项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单上，选择**项目设置**，单击**常规**底部的左窗格中，，然后选择**SQL Azure**。  
  
-   使用默认项目设置对话框中设置的所有项目的配置选项。 若要访问 SQL Azure 设置中，在**工具**菜单上，选择**DefaultProject 设置**，选择迁移项目类型作为从 SQL Azure**迁移目标版本**下拉框来访问 SQL Azure 窗格中的设置，请单击**常规**底部的左窗格中，，然后选择**SQL Azure**。  
  
## <a name="options"></a>选项  
  
## <a name="connectivity"></a>连接  
**检测信号间隔**  
  
指定要用于检测信号机制使 SQL Azure 连接中保持活动状态的时间间隔分钟： 秒的格式。  
  
**默认值**:"4:45  
  
应指定的值中正在： ss 的格式 (例如，"4:45 '或' 0:50 ')。  
  
**SQL Azure 服务器后缀**  
  
指定的 SQL Azure 服务器后缀  
  
**默认值**: database.windows.net。  
  
