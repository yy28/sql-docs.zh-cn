---
title: "连接到服务器（“连接属性”页）Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttoas.connectionproperties.f1
ms.assetid: 26cf53e3-3bcb-4697-8a88-53e93bc68b56
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6d6152b2c5deb67d4f4853a01f5831b737f00cbe
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-connection-properties-page-analysis-services"></a>连接到服务器（“连接属性”页）(Analysis Services)
当连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 或在“已注册的服务器”中注册 [!INCLUDE[ssAS](../../includes/ssas_md.md)] 时，使用此选项卡可以查看或指定选项。 进行连接时，此对话框中仅显示“连接”和“选项”。 注册 [!INCLUDE[ssAS](../../includes/ssas_md.md)] 时，此对话框中仅显示“测试”和“保存”。  
  
## <a name="options"></a>选项  
**连接到数据库**  
从列表中选择要连接到的数据库。 如果选择 **<default>**，则将连接到服务器的默认数据库。 如果选择“ **<Browse server>**”，则可以浏览服务器以查找要连接到的数据库。  
  
**连接超时值**  
输入在超时之前等待建立连接的秒数。 默认值为 15 秒。  
  
**执行超时值**  
输入在服务器上完成任务执行之前等待的时间（秒）。 默认值为零秒，指示无超时。  
  
**加密连接**  
强制对连接进行加密。  
  
**全部重置**  
将所有手动输入的连接属性值替换为默认值。  
  
**Connect**  
使用列出的值尝试连接。  
  
**选项**  
单击此项可更改对话框并隐藏其他服务器连接选项，例如记住密码。  
  
**测试**  
在“已注册的服务器”中注册 [!INCLUDE[ssAS](../../includes/ssas_md.md)] 时，单击此选项可以测试连接。  
  
**保存**  
保存“已注册的服务器”中的设置。  
  

