---
title: 使用目标助手添加目标 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 66e48903776824b0e540b854a5704ceef3a9782e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062072"
---
# <a name="add-a-destination-using-destination-assistant"></a>使用目标助手添加目标
  本主题介绍了使用目标助手添加新目标的步骤，并列出了在****“添加新目标”对话框中提供的选项，将目标助手下拉到 SSIS 设计器时可看到此对话框。  
  
### <a name="to-use-destination-assistant-to-add-a-destination"></a>使用目标助手添加目标  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要将目标组件添加到的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
2.  将 "**目标助手**" 组件从 "SSIS 工具箱" 拖动到 **"数据流" 选项卡**。应该会看到 "**添加新目标**" 对话框。 下一节提供了有关该对话框中的可用选项的详细信息。  
  
3.  在 **“类型”** 列表中，选择目标的类型。  
  
4.  在“连接管理器”列表中选择现有连接管理器，或选择“\<新建>”，创建新的连接管理器********。  
  
5.  如果您选择现有连接管理器，则单击 **“确定”** 以便关闭 **“添加新目标”** 对话框。 您应该会看到添加到数据流的目标管理器和连接管理器。  
  
6.  如果单击** \<"新建>** 创建新的连接管理器，则应该会看到"**连接管理器**"对话框，该对话框允许您指定连接的参数。 在您创建完新的连接管理器后，将在 SSIS 设计器中看到目标和连接管理器。  
  
  
