---
title: 使用控制流包部件来在包之间重用控制流 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.toolboxcontrolflowtemplate.f1
- sql13.dts.designer.addcopyexistingtemplate.f1
- sql13.dts.designer.addcopyexistingpackagepart.f1
- sql13.dts.designer.packagepart.general.f1
ms.assetid: 1edc91d9-1fab-4fe5-aed3-6f581fe32c18
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 15ba5f56b5a23b77fae66d8e4032e91a67f6a1f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65719574"
---
# <a name="reuse-control-flow-across-packages-by-using-control-flow-package-parts"></a>通过控制流包部件在包之间重用控制流

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  将常用控制流任务或容器保存到单独的部件文件“.dtsxp”中，然后即可通过控制流包部件在一个或多个包中多次重复使用它。 这种可重用性使得 SSIS 包更容易进行设计和维护。  
  
## <a name="create-a-new-control-flow-package-part"></a>创建新的控制流包部件  
 若要创建新的控制流包部件，请在解决方案资源管理器中，展开“包部件”文件夹。  右键单击“控制流”  ，然后选择“新建控制流包部件”  。  
  
 ![创建新的控制流模板](../integration-services/media/control-flow-templates-create-new.png "Create a new control flow template")  
  
 此时会在“包部件 | 控制流”文件夹中创建扩展名为“.dtsxp”的新的部件文件  。 同时，还会向 SSIS 工具箱添加具有相同名称的新项目。 （仅当你有一个包含该部件的项目且该项目在 Visual Studio 中处于打开状态时，该工具箱项目才可见。）  
  
 ![工具箱中的控制流模板](../integration-services/media/control-flow-templates-in-toolbox.png "Control flow templates in toolbox")  
  
## <a name="design-a-control-flow-package-part"></a>设计控制流包部件  
 若要打开包部件编辑器，请在解决方案资源管理器中双击部件文件。 你可以像设计包一样设计该部件。  
  
 ![控制流模板设计步骤 1](../integration-services/media/control-flow-template-design-step-1.png "Step 1 of control flow template design")  
  
 ![控制流模板设计步骤 2](../integration-services/media/control-flow-template-design-step-2.png "Step 2 of control flow template design")  
  
 控制流包部件具有以下限制。  
  
-   一个部件只能有一个顶级任务或容器。 如果你要包括多个任务或容器，可将它们都放置在单个序列容器中。  
  
-   无法在设计器中直接运行或调试部件。  
  
## <a name="add-an-existing-control-flow-package-part-to-a-package"></a>向包添加现有的控制流包部件  
 可以重用保存在当前 Integration Services 项目中或其他项目中的部件。  
  
-   若要重用属于当前项目一部分的部件，请在工具箱中拖放该部件。  
  
-   若要重用属于其他项目的部件，请使用“添加现有控制流包部件”命令。   
  
### <a name="drag-and-drop-a-control-flow-package-part"></a>拖放控制流包部件  
 若要重用项目中的部件，请直接在工具箱中拖放该部件项目，就像对任何其他任务或容器进行操作一样。 可以多次将部件拖放到包中，以便在包的多个位置重用逻辑。 通过此方法可以重用属于当前项目的部件。  
  
 ![将控制流模板添加到包](../integration-services/media/control-flow-templates-add-to-package.png "Add a control flow template to a package")  
  
 ![具有多个控制流模板的包](../integration-services/media/control-flow-templates-in-package.png "Package with multiple control flow templates")  
  
 保存包时，SSIS 设计器会检查包中是否有任何部件实例。  
  
-   如果包包含部件实例，设计器会生成新的 .dtsx.designer 文件，其中包含所有部件相关信息。  
  
-   如果包不使用部件，设计器会删除任何以前为包创建的 .dtsx.designer 文件（即任何名称与包相同的 .dtsx.designer 文件）。  
  
 ![具有控制流模板的解决方案资源管理器](../integration-services/media/control-flow-templates-in-solution-explorer.png "Solution Explorer with control flow templates")  
  
### <a name="add-a-copy-of-an-existing-control-flow-package-part-or-a-reference-to-an-existing-part"></a>添加现有控制流包部件的副本或现有部件的引用  
 若要将文件系统中现有部件的副本添加到某个包，请在解决方案资源管理器中展开“包部件”文件夹。  右键单击“控制流”  ，然后选择“添加现有控制流包部件”  。  
  
 ![从菜单中添加新的控制流模板](../integration-services/media/control-flow-templates-add-from-menu.png "Add a new control flow templates from the menu")  
  
 ![“添加现有模板副本”对话框](../integration-services/media/control-flow-templates-add-copy-dialog.png "Add Copy of Existing Templates dialog box")  
  
 **选项**  
  
 **包部件路径**  
 键入部件文件的路径或单击浏览按钮 (…)，找到要复制或引用的部件文件。  
  
 **添加为引用**  
 -   选中后，系统会将该部件作为引用添加到 Integration Services 项目。 如果你想要在多个 Integration Services 项目中引用部件文件的单个副本，则可选择此选项。  
  
-   如果清除此项，则会将部件文件的副本添加到项目。  
  
## <a name="configure-a-control-flow-package-part"></a>配置控制流包部件  
 将控制流包部件添加到包的控制流以后，若要对其进行配置，请使用“包部件配置”对话框。   
  
#### <a name="to-open-the-package-part-configuration-dialog-box"></a>打开“包部件配置”对话框的步骤  
  
1.  若要配置部件实例，请双击控制流中的部件实例。 或右键单击部件实例，然后选择“编辑”  。 此时会打开“包部件配置”对话框。   
  
2.  配置部件实例的属性和连接管理器。  
  
### <a name="properties-tab"></a>“属性”选项卡  
 使用“包部件配置”对话框的“属性”选项卡指定部件的属性。    
  
 ![“模板配置”对话框的“属性”选项卡](../integration-services/media/template-configuration-properties-tab.png "Properties tab of the Template Configuration dialog box")  
  
 左窗格中的树视图层次结构列出了部件实例的所有可配置属性。  
  
-   如果清除此项，则不会在部件实例中配置属性。 部件实例使用在控制流包部件中定义的属性的默认值。  
  
-   如果选择此项，则你输入或选择的值将覆盖默认值。  
  
 右窗格中的表会列出要配置的属性。  
  
-   **属性路径**。 属性的属性路径。  
  
-   **属性类型**。 属性的数据类型。  
  
-   **值**。 配置的值。 此值将覆盖默认值。  
  
### <a name="connection-managers-tab"></a>“连接管理器”选项卡  
 使用“包部件配置”  对话框的“连接管理器”  选项卡指定部件实例的连接管理器的属性。  
  
 ![模板配置对话框的“连接管理器”选项卡](../integration-services/media/template-configuration-connection-managers-tab.png "Connection Managers tab of the Template Configuration dialog box")  
  
 左窗格中的表列出了在控制流部件中定义的所有连接管理器。 选择要配置的连接管理器。  
  
 右窗格中的列表列出了选定连接管理器的属性。  
  
-   **设置**。 选中表示已为部件实例配置属性。  
  
-   **属性名称**。 属性的名称。  
  
-   **值**。 配置的值。 此值将覆盖默认值。  
  
## <a name="delete-a-control-flow-part"></a>删除控制流部件  
 若要删除某个部件，请在解决方案资源管理器中右键单击该部件，然后选择“删除”  。 选择“确定”确认删除，或选择“取消”保留该部件。    
  
 如果从项目中删除某个部件，将会从文件系统中永久删除该部件，且不能还原。  
  
> [!NOTE]  
>  如果要从 Integration Services 项目中删除某个部件，但要在其他项目中继续使用该部件，则可使用“从项目中排除”  选项，而不使用“删除”  选项。  
  
## <a name="package-parts-are-a-design-time-feature-only"></a>包部件仅为设计时功能  
 包部件纯粹是设计时功能。 SSIS 设计器可以在包中创建、打开、保存和更新部件，还可以添加、配置或删除部件实例。 但是，SSIS 运行时无法感知这些部件。 下面是设计器实现这种分离效果的原理。  
  
-   设计器将包部件实例及其配置的属性保存到“.dtsx.designer”文件。  
  
-   设计器在保存“.dtsx.designer”文件时，也从该文件引用的部件中提取内容，并将包中的部件实例替换为这些部件的内容。  
  
-   最后会将不再包括部件信息的所有内容重新保存到“.dtsx”包文件中。 这是 SSIS 运行时运行的文件。  
  
 下图演示了部件（“.dtsxp”文件）、SSIS 设计器和 SSIS 运行时之间的关系。  
  
 ![控制流模板文件和流](../integration-services/media/control-flow-templates-intro.png "Control flow templates files and flow")  
  
  
