---
title: 源助手 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a445bafcb6182f4af0d6089085c5a579b9109d7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917793"
---
# <a name="source-assistant"></a>源助手

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  源助手组件可以帮助创建源组件和连接管理器。 该组件位于 SSIS 工具箱的 **“收藏夹”** 部分中。  
  
> [!NOTE]  
>  源助手替换 Integration Services 连接项目和相应向导。  
  
## <a name="add-a-source-with-source-assistant"></a>使用源助手添加源
本节介绍了使用源助手添加新源的步骤，并且列出了在“添加新源”对话框中提供的选项，将源助手向下拉到 SSIS 设计器时可看到此对话框  。  

1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要将源组件添加到的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  将 **“源助手”** 组件从 SSIS 工具箱拖到 **“数据流”** 选项卡。您应该会看到 **“添加新源”** 对话框。 下一节提供了有关该对话框中的可用选项的详细信息。  
  
3.  在 **“类型”** 列表中，选择目标的类型。  
  
4.  在“连接管理器”列表中选择现有连接管理器，或选择“\<New>”以创建新的连接管理器 。  
  
5.  如果您选择现有连接管理器，则单击 **“确定”** 以便关闭 **“添加新目标”** 对话框。 您应该会看到添加到数据流的目标管理器和连接管理器。  
  
6.  如果单击“\<New>”创建新的连接管理器，则应该会看到“连接管理器”对话框，你看从中指定连接的参数 。 在您创建完新的连接管理器后，将在 SSIS 设计器中看到目标和连接管理器。  

## <a name="add-new-source-dialog-box"></a>“添加新源”对话框
下表列出了“添加新源”对话框中的可用选项  。  
  
|选项|说明|  
|------------|-----------------|  
|类型|选择要连接到的源的类型。|  
|连接管理器|选择现有连接管理器，或单击“\<New>”以创建新的连接管理器。|  
|仅显示已安装项|指定是否要仅查看安装的源。|  
|OK|单击以保存您的更改，并打开任何后续对话框来配置其他选项。| 
  
