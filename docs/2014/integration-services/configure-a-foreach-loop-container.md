---
title: 配置 Foreach 循环容器 |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d63a4f168c4a426c06bb00c634f89e328735332
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159757"
---
# <a name="configure-a-foreach-loop-container"></a>配置 Foreach 循环容器
  此过程介绍如何配置 Foreach 循环容器，包括如何在枚举器级和容器级上配置属性表达式。  
  
### <a name="to-configure-the-foreach-loop-container"></a>配置 Foreach 循环容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  单击“控制流”选项卡，然后双击 Foreach 循环。  
  
3.  在 **“Foreach 循环编辑器”** 对话框中，单击 **“常规”** ，并且，根据需要还可以修改 Foreach 循环的名称和说明。  
  
4.  单击 **“集合”** ，然后从 **“枚举器”** 列表中选择一个枚举器类型。  
  
5.  指定一个枚举器并对枚举器选项进行如下设置：  
  
    -   若要使用 Foreach 文件枚举器，请提供包含要枚举的文件的文件夹，指定文件名和文件类型筛选器，并指定是否返回完全合格的文件名。 另外，还请指定是否包含子文件夹，以枚举更多文件。  
  
    -   若要使用 Foreach 项枚举器，请单击 **“列”**，然后在 **“For Each Item 列”** 对话框中，单击 **“添加”** 来添加列。 在 **“数据类型”** 列表中为每个列选择一个数据类型，然后单击 **“确定”**。  
  
         在列中键入值或从列表中选择值。  
  
        > [!NOTE]  
        >  若要添加新行，请在刚才输入的单元格之外，单击任一位置。  
  
        > [!NOTE]  
        >  如果值与列数据类型不兼容，文本将突出显示。  
  
    -   若要使用 Foreach ADO 枚举器，请选择一个现有的变量，或在 **“ADO 对象源变量”** 列表，单击 **“新建变量”** 来指定一个变量（包含要枚举的 ADO 对象的名称），然后选择一个枚举模式选项。  
  
         如果要创建新变量，请在 **“添加变量”** 对话框中设置该变量的属性。  
  
    -   若要使用 Foreach ADO.NET 架构行集枚举器，请选择一个现有的 ADO.NET 连接，或在 **“连接”** 列表中，单击 **“新建连接”** ，然后选择一个架构。  
  
         也可以单击 **“设置限制”** ，选择架构限制，选择包含限制值的变量，或键入限制值，然后单击 **“确定”**。  
  
    -   若要使用 Foreach 源变量枚举器，请在 **“变量”** 列表中选择变量。  
  
    -   若要使用 Foreach NodeList 枚举器，请单击 DocumentSourceType 并从列表中选择源类型，然后单击 DocumentSource。 根据为 DocumentSourceType 选择的值，请从列表中选择变量或文件连接，或创建新变量或文件连接，或在“文档源编辑器”中键入 XML 源代码。  
  
         接下来，单击 EnumerationType 并从列表中选择枚举类型。 如果 EnumerationType 是 **Navigator、Node 或 NodeText**，则单击 OuterXPathStringSourceType 并选择源类型，然后单击 OuterXPathString。 根据为 OuterXPathStringSourceType 设置的值，请从列表中选择变量或文件连接，或创建新的变量或文件连接，或键入外部 XML 路径语言 (XPath) 表达式的字符串。  
  
         如果 EnumerationType 是 **ElementCollection**，则按上文所述设置 OuterXPathStringSourceType 和 OuterXPathString。 然后，单击 InnerElementType 并选择内部元素的枚举类型，然后单击 InnerXPathStringSourceType。 根据为 InnerXPathStringSourceType 设置的值，请选择变量或文件连接，创建新的变量或文件连接，或键入内部 XPath 表达式的字符串。  
  
    -   若要使用 Foreach SMO 枚举器，请选择一个现有的 ADO.NET 连接，或在 **“连接”** 列表中，单击 **“新建连接”** ，然后键入需要的字符串或单击 **“浏览”**。 如果选择单击 **“浏览”**，则请在 **“选择 SMO 枚举”** 对话框中，选择要枚举的对象类型和枚举类型，然后单击 **“确定”**。  
  
6.  也可单击“集合”页上的“表达式”文本框中的浏览按钮 **(…)** 来创建可用于更新属性值的表达式。 有关详细信息，请参阅[添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)。  
  
    > [!NOTE]  
    >  在“属性”列表中列出的属性因枚举器而异。  
  
7.  也可以单击 **“变量映射”** ，将对象属性映射到集合值，然后进行下列操作：  
  
    1.  在“变量”列表中选择变量，或单击 \<“新建变量”> 创建新的变量。  
  
    2.  如果要添加新变量，那么请在 **“添加变量”** 对话框中设置该变量的属性，然后单击 **“确定”**。  
  
    3.  如果使用 For Each Item 枚举器，可以在 **“索引”** 列表中来更新索引值。  
  
        > [!NOTE]  
        >  该索引值指示项中哪个列将映射到变量。 只有 For Each Item 枚举器可以使用 0 以外的索引值。  
  
8.  也可以单击 **“表达式”** ，然后在 **“表达式”** 页上，为 Foreach 循环容器的属性创建属性表达式。 有关详细信息，请参阅 [添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)。  
  
9. 单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [Foreach 循环容器](control-flow/foreach-loop-container.md)  
  
  
