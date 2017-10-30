---
title: "源助手 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9b7406edf9f7234db739730473772d77c42399ec
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="source-assistant"></a>源助手
  源助手组件可以帮助创建源组件和连接管理器。 该组件位于 SSIS 工具箱的 **“收藏夹”** 部分中。  
  
> [!NOTE]  
>  源助手替换 Integration Services 连接项目和相应向导。  
  
## <a name="add-a-source-with-source-assistant"></a>添加带有源助手的源
此部分提供要添加新的源使用源助手步骤，并还列出可用的选项**添加新源**对话框，你将看到当你拖放到 SSIS 设计器的助手源。  

1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要将源组件添加到的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  将 **“源助手”** 组件从 SSIS 工具箱拖到 **“数据流”** 选项卡。您应该会看到 **“添加新源”** 对话框。 下一节提供了有关该对话框中的可用选项的详细信息。  
  
3.  在 **“类型”** 列表中，选择目标的类型。  
  
4.  选择现有连接管理器中的**连接管理器**列表或选择**\<新建 >**创建新的连接管理器。  
  
5.  如果您选择现有连接管理器，则单击 **“确定”** 以便关闭 **“添加新目标”** 对话框。 您应该会看到添加到数据流的目标管理器和连接管理器。  
  
6.  如果你单击**\<新建 >**若要创建新的连接管理器，你应看到**连接管理器**对话框中，可以指定连接参数。 在您创建完新的连接管理器后，将在 SSIS 设计器中看到目标和连接管理器。  

## <a name="add-new-source-dialog-box"></a>添加新源对话框
下表列出了中的可用选项**添加新源**对话框。  
  
|选项|Description|  
|------------|-----------------|  
|类型|选择要连接到的源的类型。|  
|连接管理器|选择一个现有的连接管理器，或单击**\<新建 >**创建新的连接管理器。|  
|仅显示已安装项|指定是否要仅查看安装的源。|  
|确定|单击以保存您的更改，并打开任何后续对话框来配置其他选项。| 
  

