---
title: 添加源使用源助手 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5e850b7c-4b89-42ad-b0a6-d63ac7cc9568
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b162ebfa6d888460b49f0877d634c88bba47464a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062140"
---
# <a name="add-a-source-using-source-assistant"></a>使用源助手添加源
  本主题介绍了使用源助手添加新源的步骤，并且列出了在“添加新源”  对话框中提供的选项，将源助手向下拉到 SSIS 设计器时可看到此对话框。  
  
### <a name="to-use-source-assistant-to-add-a-source"></a>使用源助手添加源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要将源组件添加到的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
2.  将 **“源助手”** 组件从 SSIS 工具箱拖到 **“数据流”** 选项卡。您应该会看到 **“添加新源”** 对话框。 下一节提供了有关该对话框中的可用选项的详细信息。  
  
3.  在 **“类型”** 列表中，选择目标的类型。  
  
4.  在“连接管理器”列表中选择现有连接管理器，或选择“\<新建>”，创建新的连接管理器   。  
  
5.  如果您选择现有连接管理器，则单击 **“确定”** 以便关闭 **“添加新目标”** 对话框。 您应该会看到添加到数据流的目标管理器和连接管理器。  
  
6.  如果单击“\<新建>”创建新的连接管理器，可看到“连接管理器”对话框，可在其中指定连接参数   。 在您创建完新的连接管理器后，将在 SSIS 设计器中看到目标和连接管理器。  
  
  
