---
title: 脚本组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponentdetails.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65a5c846313ad6d7d840c272c23c16698530547f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437554"
---
# <a name="script-component"></a>脚本组件
  脚本组件承载脚本，并使包能够包含和运行自定义的脚本代码。 可以将包中的脚本组件用于下列目的：  
  
-   将多个转换应用于数据，而不是在数据流中使用多个转换。 例如，脚本可以将两列中的值相加，然后计算和的平均值。  
  
-   访问现有 .NET 程序集中的业务规则。 例如，脚本可以应用指定 `Income` 列中有效值范围的业务规则。  
  
-   除 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 表达式语法提供的函数和运算符之外，还可使用自定义公式和函数。 例如，使用 LUHN 公式验证信用卡号。  
  
-   验证列数据，并跳过包含无效数据的记录。 例如，脚本可以评估邮资额的合理性，并跳过金额过高或过低的记录。  
  
 脚本组件为将自定义函数纳入数据流提供了简便快捷的方法。 但是，如果您计划在多个包中重新使用脚本代码，则应考虑编写自定义组件，而不使用脚本组件。 有关详细信息，请参阅 [开发自定义数据流组件](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
> [!NOTE]  
>  如果脚本组件包含尝试读取 NULL 列值的脚本，则在您运行包时此脚本组件将失败。 建议你的脚本先使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> 方法确定相应列是否为 NULL，再尝试读取该列的值。  
  
 脚本组件可用作源、转换或目标。 该组件支持一个输入和多个输出。 根据其使用方式，该组件可以支持一个输入或多个输出，也可二者都支持。 脚本由输入或输出中的每一行调用。  
  
-   如果用作源，则脚本组件支持多个输出。  
  
-   如果用作转换，则脚本组件支持一个输入和多个输出。  
  
-   如果用作目标，则脚本组件支持一个输入。  
  
 脚本组件不支持错误输出。  
  
 确定将此脚本组件作为包的正确选择之后，必须配置输入和输出、开发该组件使用的脚本并配置组件本身。  
  
## <a name="understanding-the-script-component-modes"></a>了解脚本组件模式  
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中，脚本组件具有两种模式：元数据设计模式和代码设计模式。 在元数据设计模式中，可以添加和修改脚本组件的输入和输出，但不能编写代码。 配置完所有的输入和输出后，即可切换至代码设计模式编写脚本。 脚本组件从输入和输出的元数据自动生成基代码。 如果在脚本组件生成基代码后更改元数据，则您的代码可能无法再编译，因为更新的基代码可能与您的代码不兼容。  
  
## <a name="writing-the-script-that-the-component-uses"></a>编写组件使用的脚本  
 脚本组件将 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 用作编写脚本的环境。 您可以从 **“脚本转换编辑器”** 访问 VSTA。 有关详细信息，请参阅 [脚本转换编辑器（“脚本”页）](../../script-transformation-editor-script-page.md)。  
  
 脚本组件提供一个 VSTA 项目，其中包含一个名为 ScriptMain 的自动生成的类，表示组件元数据。 例如，如果将脚本组件用作具有三个输出的转换，则 ScriptMain 为每个输出都包含一种方法。 ScriptMain 是脚本的入口点。  
  
 VSTA 包含 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 环境的所有标准功能，如具有颜色编码的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 编辑器、IntelliSense 和对象浏览器。 脚本组件使用的脚本存储在包定义中， 设计包时，脚本代码将临时写入项目文件。  
  
 VSTA 支持 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 编程语言。  
  
 有关如何对脚本组件进行编程的信息，请参阅 [使用脚本组件扩展数据流](script-component.md)。 有关如何将脚本组件配置为源、转换或目标的更多特定信息，请参阅 [Developing Specific Types of Script Components](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。 有关说明脚本组件使用的其他示例（如 ODBC 目标），请参阅 [Additional Script Component Examples](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。  
  
> [!NOTE]  
>  在早期版本中您可以指示是否对脚本进行预编译，而在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 和更高版本中，不同的是，所有脚本都要预编译。 脚本进行预编译后，运行时将不加载语言引擎，因此包运行得更快。 但是，预编译二进制文件占用了大量的磁盘空间。  
  
## <a name="configuring-the-script-component"></a>配置脚本组件  
 可以采用下列方法来配置脚本组件：  
  
-   选择要引用的输入列。  
  
    > [!NOTE]  
    >  使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器时，可以仅配置一个输入。  
  
-   提供组件运行的脚本。  
  
-   指定脚本语言。  
  
-   提供逗号分隔的只读和读/写变量列表。  
  
-   添加更多输出，并且添加脚本要向其赋值的输出列。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
### <a name="configuring-the-script-component-in-the-designer"></a>配置设计器中的脚本组件  
 有关可在 **“脚本转换编辑器”** 对话框中设置的属性的详细信息，请单击以下主题之一：  
  
-   [脚本转换编辑器（“输入列”页）](../../script-transformation-editor-input-columns-page.md)  
  
-   [脚本转换编辑器（“输入和输出”页）](../../script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [脚本转换编辑器（“脚本”页）](../../script-transformation-editor-script-page.md)  
  
-   [脚本转换编辑器（“连接管理器”页）](../../script-transformation-editor-connection-managers-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>以编程方式配置脚本组件  
 有关可在 **“属性”** 窗口中或以编程形式设置的属性的详细信息，请单击以下主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
 [Integration Services 转换](integration-services-transformations.md)  
  
 [Extending the Data Flow with the Script Component](script-component.md)  
  
  
