---
title: 在维度设计器中查看特性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eb12bd6499796ff7f2cfb09ccd4c176914c8117
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175796"
---
# <a name="view-attributes-in-dimension-designer"></a>在维度设计器中查看属性
  属性是针对维度对象创建的。 您可以使用中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的维度设计器来查看和配置属性。 维度设计器的 **“维度结构”** 选项卡的 **“属性”** 窗格中列出了维度中的各属性。 使用该窗格可以添加、删除或配置属性。 您还可以选择属性以将其用作新建层次结构中的某一级别，或添加为现有层次结构中的某一级别。

 若要查看维度中的属性，请打开该维度的维度设计器。 该设计器的 **“维度结构”** 选项卡的 **“属性”**  窗格中显示了维度中的各属性。 您可以通过以下方式在列表、树或网格视图之间进行切换：指向的 "**维度**" 菜单上[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 "**显示属性**"，然后单击下表中所示的某个命令。

|属性显示方式|说明|
|------------------------|-----------------|
|**成员列表**|以列表格式显示属性。<br /><br /> 右键单击要从列表中删除的属性以重命名该属性，或更改其用法。<br /><br /> 使用该视图可以生成层次结构。 特性信息和成员属性不可见。|
|**树**|以树格式显示属性，其中维度作为树中的顶级节点。 使用该视图可以查看和创建成员属性。 您还可以使用该视图生成层次结构。 展开属性可以查看其属性关系，还可以通过执行下列操作创建新的属性关系：<br /><br /> 在 **“属性”** 窗口中单击要查看其属性的维度、特性或成员属性。<br /><br /> 右键单击要从列表中删除的特性或成员属性以重命名该特性或成员属性，或更改其用法。|
|**格**|以网格格式显示属性。 单击网格中的任意行便可查看该特性的属性。  使用该视图可以创建和配置属性。 该网格显示下列各列：<br /><br /> **名称**：显示**name**属性的值。 键入其他名称可以更改该设置。<br /><br /> **用法**：指定此属性是常规属性、键属性、父属性还是 AccountType 属性。 单击该列中的值便可选择其他设置。<br /><br /> **类型**：指定属性的商业智能类别。 单击该单元便可选择其他设置。<br /><br /> **键列**：显示特性的**KeyColumn**属性的 OLE DB 数据类型。 该列无法更改。<br /><br /> **名称列**：指示特性的**NameColumn**属性设置是否与**KeyColumn**属性的设置相同。 该列无法更改。|

 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，下表中显示的图标根据属性的用法对属性进行标记。

|图标|属性用法|
|----------|---------------------|
|![属性图标](../media/as-icon-attribute.gif "属性图标")|常规或 AccountType|
|![键属性图标](../media/as-icon-key-attribute.gif "键属性图标")|密钥|
|![父属性图标](../media/as-icon-parent-attribute.gif "父属性图标")|Parent|

## <a name="see-also"></a>另请参阅
 [维度特性属性参考](dimension-attribute-properties-reference.md)


