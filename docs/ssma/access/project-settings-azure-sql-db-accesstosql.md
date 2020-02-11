---
title: 项目设置（Azure SQL DB）（AccessToSQL） |Microsoft Docs
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
ms.openlocfilehash: 60140559f94cdeebea935b423fbbeef24bce7a08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67929460"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>项目设置（Azure SQL DB）（AccessToSQL）
SQL Azure 项目设置允许您配置要添加到连接对话框中的 SQL Azure 数据库后缀，还允许在 SQL Azure 连接中实现检测信号机制。  
  
"SQL Azure" 窗格在 "**项目设置**" 和 "**默认项目设置**" 对话框中可用。  
  
-   使用 "项目设置" 对话框可以设置当前项目的配置选项。 若要访问 SQL Azure 设置，请在 "**工具**" 菜单上选择 "**项目设置**"，单击左侧窗格底部的 "**常规**"，然后选择 " **SQL Azure**"。  
  
-   使用 "默认项目设置" 对话框可以为所有项目设置配置选项。 若要访问 SQL Azure 设置，请在 "**工具**" 菜单上选择 " **DefaultProject 设置**"，在 "**迁移目标版本**" 组合框中选择 "SQL Azure" 项目类型以访问 SQL Azure 窗格中的设置，单击左窗格底部的 "**常规**"，然后选择 " **SQL Azure**"。  
  
## <a name="options"></a>选项  
  
## <a name="connectivity"></a>连接  
**检测信号间隔**  
  
指定一个时间间隔，该时间间隔用于检测信号机制以使 SQL Azure 连接以 "分钟：秒" 格式保持活动状态。  
  
**默认值**： "4:45"  
  
应以 "m:ss" 格式（例如，"4:45" 或 "0:50"）指定值。  
  
**SQL Azure 服务器后缀**  
  
指定 SQL Azure 服务器后缀  
  
**默认值**： "database.windows.net"。  
  
