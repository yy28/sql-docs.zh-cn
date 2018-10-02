---
title: 目标助手 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 52fdfd7647af5146f2c2c5c06d5127e5562bb392
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689735"
---
# <a name="destination-assistant"></a>目标助手
  目标助手组件可以帮助创建目标组件和连接管理器。 该组件位于 SSIS 工具箱的 **“收藏夹”** 部分中。  
  
> [!NOTE]  
>  目标助手替换 Integration Services 连接项目和相应向导。  

## <a name="add-a-destination-with-destination-assistant"></a>使用目标助手添加目标
本主题介绍了使用目标助手添加新目标的步骤，并列出了在“添加新目标”对话框中提供的选项，将目标助手下拉到 SSIS 设计器时可看到此对话框。  

1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要将目标组件添加到的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  将 **“目标助手”** 组件从 SSIS 工具箱拖到 **“数据流”** 选项卡。您应该会看到 **“添加新目标”** 对话框。 下一节提供了有关该对话框中的可用选项的详细信息。  
  
3.  在 **“类型”** 列表中，选择目标的类型。  
  
4.  在“连接管理器”列表中选择现有连接管理器，或选择“\<新建>”，创建新的连接管理器。  
  
5.  如果您选择现有连接管理器，则单击 **“确定”** 以便关闭 **“添加新目标”** 对话框。 您应该会看到添加到数据流的目标管理器和连接管理器。  
  
6.  如果单击“\<新建>”创建新的连接管理器，可看到“连接管理器”对话框，可在其中指定连接参数。 在您创建完新的连接管理器后，将在 SSIS 设计器中看到目标和连接管理器。 
  
## <a name="add-new-destination-dialog-box"></a>“添加新目标”对话框
下表列出了“添加新目标”对话框的可用选项。  
  
|选项|描述|  
|------------|-----------------|  
|类型|选择要连接到的目标的类型。|  
|连接管理器|选择现有连接管理器或单击“\<新建>”创建新的连接管理器。|  
|仅显示已安装项|指定是否要仅查看安装的目标。|  
|“确定”|单击以保存您的更改，并打开任何后续对话框来配置其他选项。|  
