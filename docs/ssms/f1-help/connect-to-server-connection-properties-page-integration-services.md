---
title: "连接到 SSIS 服务器（连接属性）| Microsoft Docs"
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
- sql13.ssiseditserverregistration.connectionproperties.f1
- sql13.swb.connecttodts.connectionproperties.f1
ms.assetid: c2513dab-8415-4e0c-9475-6d4ab97fea7c
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 734f14076b65d0ea7e4c26c95c463a3554828587
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-connection-properties-page-integration-services"></a>连接到服务器（“连接属性”页）(Integration Services)
当连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] 或在“已注册的服务器”中注册 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 时，使用此选项卡可以查看或指定选项。 进行连接时，此对话框中仅显示“连接”和“选项”。 注册 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 时，此对话框中仅显示“测试”和“保存”。  
  
## <a name="options"></a>选项  
**端口号**  
输入 [!INCLUDE[ssIS](../../includes/ssis_md.md)]使用的端口号。  
  
**连接超时**  
输入在超时之前等待建立连接的秒数。 默认值为 15 秒。  
  
**执行超时值**  
输入在服务器上完成任务执行之前等待的时间（秒）。 默认值为零秒，指示无超时。  
  
**全部重置**  
将所有手动输入的连接属性值替换为默认值。  
  
**Connect**  
使用列出的值尝试连接。  
  
**选项**  
单击此项可更改对话框并隐藏其他服务器连接选项，例如记住密码。  
  
**测试**  
在“已注册的服务器”中注册 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 时，单击此选项可以测试连接。  
  
**保存**  
保存“已注册的服务器”中的设置。  
  

