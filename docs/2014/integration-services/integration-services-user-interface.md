---
title: Integration Services 用户界面 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55b09057927fa9c5102b8d816c42e1741bc0883a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767669"
---
# <a name="integration-services-user-interface"></a>Integration Services 用户界面
  除了 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器选项卡上的设计图面外，还可通过用户界面访问下面的窗口和对话框，以便向包添加功能以及配置包对象的属性。  
  
-   用于向包添加功能（如记录日志和配置）的对话框和窗口。  
  
-   配置包对象属性的自定义编辑器。 几乎每种类型的容器、任务和数据流组件都有其自己的自定义编辑器。  
  
-   **“高级编辑器”** 对话框，这是为许多数据流组件提供更详细的配置选项的通用编辑器。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 还提供了用于配置环境和对包进行操作的窗口和对话框。  
  
## <a name="dialog-boxes-and-windows"></a>对话框和窗口  
 在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包或创建新包后，便可使用下列对话框和窗口。  
  
 此表列出可从 **SSIS** 菜单和 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的设计图面访问的对话框。  
  
|对话框|目的|访问|  
|----------------|-------------|------------|  
|**入门**|访问示例、教程和视频内容。|右键单击“控制流”  选项卡或“数据流”  选项卡的设计图面，然后单击“入门”  。<br /><br /> 要在创建新的 **项目时自动显示** “入门” [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 窗口，请选择该窗口底部的 **“始终在新项目中显示”** 。|  
|**配置 SSIS 日志**|添加日志和设置日志记录详细信息，从而配置包及其任务的日志记录。|在 **SSIS** 菜单上，单击 **“日志记录”** 。<br /><br /> -或-<br /><br /> 右键单击“控制流”  选项卡的设计图面上任意位置，再单击“日志记录”  。|  
|**包配置组织程序**|添加和编辑包配置。 请从此对话框运行包配置向导。|在 **SSIS** 菜单上，单击 **“包配置”** 。<br /><br /> -或-<br /><br /> 右键单击“控制流”  选项卡的设计图面上任意位置，再单击“包配置”  。|  
|**数字签名**|为包签名或从包中删除签名。|在 **SSIS** 菜单上，单击 **“数字签名”** 。<br /><br /> -或-<br /><br /> 右键单击“控制流”  选项卡的设计图面上任意位置，再单击“数字签名”  。|  
|**设置断点**|对任务启用断点，并设置断点属性。|在“控制流”  选项卡的设计图面上，右键单击任务或容器，再单击“编辑断点”  。 若要对包设置断点，请右键单击“控制流”  选项卡的设计图面上的任意位置，再单击“编辑断点”  。|  
  
 **“入门”** 窗口提供指向示例、教程和视频内容的链接。 若要添加指向更多内容的链接，请修改 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]当前版本附带的 SamplesSites.xml 文件。 建议不要修改指定 RSS 源 URL 的 \<GettingStartedSamples> 元素值。 该文件位于 *drive>:\Program Files\Microsoft SQL Server\110\DTS\Binn 文件夹中\<* 。 在 64 位计算机上，该文件位于 *drive>:\Program Files(x86)\Microsoft SQL Server\110\DTS\Binn 文件夹中\<* 。  
  
 如果 SamplesSites.xml 文件确已损坏，请用下面的默认 xml 替换该文件中的 xml。  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>https://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>https://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 此表列出可从 **SSIS** 和 **“视图”** 菜单以及 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的设计图面访问的窗口。  
  
|窗口|目的|访问|  
|------------|-------------|------------|  
|**变量**|添加和管理自定义变量。|在 **SSIS** 菜单上单击 **“变量”** 。<br /><br /> -或-<br /><br /> 右键单击“控制流”  和“数据流”  选项卡的设计图面上任意位置，再单击“变量”  。<br /><br /> -或-<br /><br /> 在 **“视图”** 菜单上，指向 **“其他窗口”** ，再单击 **“变量”** 。|  
|**日志事件**|在运行时查看日志项。|在 **SSIS** 菜单上单击 **“日志事件”** 。<br /><br /> -或-<br /><br /> 右键单击“控制流”  和“数据流”  选项卡的设计图面上的任意位置，再单击“日志事件”  。<br /><br /> -或-<br /><br /> 在 **“视图”** 菜单上指向 **“其他窗口”** ，再单击 **“日志事件”** 。|  
  
## <a name="custom-editors"></a>自定义编辑器  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 为大多数容器、任务、源、转换和目标提供了自定义对话框。  
  
 下表介绍如何访问自定义对话框。  
  
|编辑器类型|访问|  
|-----------------|------------|  
|容器。 有关详细信息，请参阅 [Integration Services 容器](control-flow/integration-services-containers.md)。|在“控制流”  选项卡的设计图面上，双击容器。|  
|任务。 有关详细信息，请参阅 [Integration Services Tasks](control-flow/integration-services-tasks.md)。|在“控制流”  选项卡的设计图面上，双击任务。|  
|源。|在“数据流”  选项卡的设计图面上，双击源。|  
|转换。 有关详细信息，请参阅 [Integration Services Transformations](data-flow/transformations/integration-services-transformations.md)。|在“数据流”  选项卡的设计图面上，双击转换。|  
|目标。|在“数据流”  选项卡的设计图面上，双击目标。|  
  
## <a name="advanced-editor"></a>“高级编辑器”  
 **“高级编辑器”** 对话框是用于配置数据流组件的用户界面。 它使用通用的布局反映组件的属性。 **“高级编辑器”** 对话框对具有多个输入的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 转换不可用。  
  
 若要打开此编辑器，请单击“属性”  窗口中的“显示高级编辑器”  ，或右键单击数据流组件，再单击“显示高级编辑器”  。  
  
 如果创建自定义源、转换或目标，但不想编写自定义用户界面，则可以使用 **“高级编辑器”** 。  
  
## <a name="sql-server-data-tools-features"></a>SQL Server Data Tools 功能  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供用于对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包进行操作的窗口、对话框和菜单选项。  
  
 以下是可用窗口和菜单的摘要：  
  
-   **“解决方案资源管理器”** 窗口列出项目（包括用于开发 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目）和项目文件。  
  
     若要按项目中包含的包的名称排序，请右键单击“SSIS 包”  节点，然后单击“按名称排序”  。  
  
-   **“工具箱”** 窗口列出用于生成控制流和数据流的控制流项和数据流项。  
  
-   **“属性”** 窗口列出对象属性。  
  
-   **“格式”** 菜单提供用于在包中调整控件大小和对齐控件的选项。  
  
-   **“编辑”** 菜单提供在设计图面上复制对象的复制和粘贴功能。  
  
-   **“视图”** 菜单提供用于在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中修改对象图形表现形式的选项。  
  
 有关其他窗口和菜单的详细信息，请参阅 Visual Studio 文档。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建包的信息，请参阅 [在 SQL Server Data Tools 中创建包](create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>另请参阅  
 [SSIS 设计器](ssis-designer.md)  
  
  
