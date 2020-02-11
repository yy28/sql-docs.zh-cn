---
title: 项目设置（Azure SQL DB）（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 829e7b0c51cd341193944fb2f28241f48618c407
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176224"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>项目设置 (Azure SQL DB) (SybaseToSQL)
利用 Azure SQL 数据库项目设置，你可以配置要添加到连接对话框中的 Azure SQL DB 数据库后缀，还允许在 Azure SQL DB 连接中实现检测信号机制。  
  
"**项目设置**" 和 "**默认项目设置**" 对话框中提供了 "Azure SQL 数据库" 窗格。  
  
-   使用 "项目设置" 对话框可以设置当前项目的配置选项。 若要访问 Azure SQL DB 设置，请在 "**工具**" 菜单上选择 "**项目设置**"，单击左侧窗格底部的 "**常规**"，然后选择 " **Azure sql DB**"。  
  
-   使用 "默认项目设置" 对话框可以为所有项目设置配置选项。 若要访问 Azure SQL DB 设置，请在 "**工具**" 菜单上选择 " **DefaultProject 设置**"，单击左侧窗格底部的 "**常规**"，然后选择 " **Azure sql DB**"。  
  
## <a name="connectivity"></a>连接  
**检测信号间隔**  
  
指定一个时间间隔，该时间间隔用于检测信号机制以使 Azure SQL DB 连接以 "分钟：秒" 格式保持活动状态。  
  
**默认值**： "4:45"  
  
应以 "m:ss" 格式（例如，"4:45" 或 "0:50"）指定值。  
  
**Azure SQL DB 服务器后缀**  
  
指定 Azure SQL DB 服务器后缀  
  
**默认值**： "database.windows.net"。  
  
