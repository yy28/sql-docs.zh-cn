---
title: 修复分布式的重播安装 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d14b1bf3200802e9fab359ba3ede9fa295911fe1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227207"
---
# <a name="repair-a-distributed-replay-installation"></a>修复 Distributed Replay 安装
  修复 Distributed Replay 组件（控制器或客户端）时将执行以下操作：  
  
1.  在磁盘上再次安装所有关联的文件，并替换所有现有文件。  
  
2.  重新创建 Windows 服务帐户（如果相应的服务帐户已删除）。  
  
 您无法使用修复操作添加或删除组件。 若要添加或删除组件，请选中或取消选中上的功能树中的对应分量**功能选择**页中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序。  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>修复失败的 Distributed Replay 安装  
  
1.  从**启动**菜单上，单击**控制面板**，然后双击**添加或删除程序**。  
  
2.  选择[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中**卸载或更改程序**窗口中，然后在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]对话框中，单击**修复**。  
  
3.  按照中的步骤[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]向导中，然后在**选择功能**页上，选择你想要修复，然后单击 Distributed Replay 组件**下一步。**。  
  
4.  完成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导以修复选定的 Distributed Replay 功能。  
  
  
