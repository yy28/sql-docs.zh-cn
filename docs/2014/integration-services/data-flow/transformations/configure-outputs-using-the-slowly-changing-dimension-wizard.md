---
title: 使用渐变维度向导配置输出 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- Slowly Changing Dimension Wizard
ms.assetid: da111731-1ffa-49b9-bcaa-3c93fd0eb619
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79ae2c560bfc5e5e38d46e72bad0b1a734421ee5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085417"
---
# <a name="configure-outputs-using-the-slowly-changing-dimension-wizard"></a>使用渐变维度向导配置输出
  渐变维度向导所起作用相当于渐变维度转换的编辑器。 为渐变维度数据生成和配置数据流可能是一项复杂的任务。 渐变维度向导提供了为渐变维度转换输出生成数据流的最简便方法，指导您逐步完成映射列、选择业务键列、设置列更改属性以及配置对推断维度成员的支持。  
  
 必须在维度表中选择至少一个业务键列，并将其映射到输入列。 业务键的值将源中的一条记录链接到维度表中的一条记录。 转换使用此映射在维度表中定位该记录，并确定某条记录是新的还是更改过的。 业务键通常是源中的主键。如果业务键唯一标识一条记录而且其值不改变，则它也可以作为备用键。 业务键还可以是由多列构成的组合键。 维度表中的主键通常是代理键，它表示标识列或自定义解决方案（如脚本）自动生成的数值。  
  
 必须向数据流添加源和渐变维度转换，再将源的输出连接到渐变维度转换的输入，然后才能运行渐变维度向导。 数据流还可以在数据源和渐变维度转换之间包含其他转换。  
  
 若要在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中打开渐变维度向导，请双击渐变维度转换。  
  
## <a name="creating-slowly-changing-dimension-outputs"></a>创建渐变维度输出  
  
#### <a name="to-create-slowly-changing-dimension-transformation-outputs"></a>创建渐变维度转换输出  
  
1.  选择连接管理器，以便访问包含要更新的维度表的数据源。  
  
     可以从包所包含的连接管理器列表中选择。  
  
2.  选择要更新的维度表或视图。  
  
     选择连接管理器后，可以从数据源选择表或视图。  
  
3.  设置列的键属性，并将输入列映射到维度表中的列。  
  
     必须在维度表中选择至少一个业务键列，并将其映射到输入列。 其他输入列可以作为非键映射映射到维度表中的列。  
  
4.  选择每列的更改类型。  
  
    -   **“变化的属性”** 覆盖记录中的现有值。  
  
    -   **“历史属性”** 创建新记录而不更新现有记录。  
  
    -   **“固定的属性”** 指示列值不得更改。  
  
5.  设置固定和变化的属性选项。  
  
     如果将列配置为使用 **“固定的属性”** 更改类型，则可以指定在这些列中检测到更改时渐变维度转换是否失败。 如果将列配置为使用 **“变化的属性”** 更改类型，则可以指定是否更新包括过期记录在内所有匹配的记录。  
  
6.  设置历史属性选项。  
  
     如果将列配置为使用 **“历史属性”** 更改类型，则必须选择如何区分当前记录和过期记录。 可以使用一个当前行指示器列或两个日期列来标识当前行和过期行。 如果使用当前行指示器列，则可以将其设置成当行是当前行时为 **“当前”** 或 **True** ，而当行是过期行时为 **“过期”** 或 **False** 。 也可以输入自定义值。 如果使用两个日期列（开始日期和结束日期），则可以输入日期或选择系统变量然后使用其值，从而指定设置日期列值时要使用的日期。  
  
7.  指定对推断成员的支持，并选择推断成员记录所包含的列。  
  
     向事实数据表中加载度量值时，可以为尚不存在的推断成员创建最小记录。 以后出现有意义的数据时，可以更新维度记录。 可以创建以下类型的最小记录：  
  
    -   其中所有带更改类型的列中的记录均为空。  
  
    -   其中有布尔值列指示该记录为推断成员的记录。  
  
8.  检查渐变维度向导生成的配置。 根据所支持的更改类型，将不同的数据流组件集添加到包。  
  
     下列关系图所示的示例数据流支持固定的属性更改、变化的属性更改以及历史属性更改、推断成员和对匹配记录的更改。  
  
     ![渐变维度向导的数据流](../../media/dimensionwizard.gif "Data flow from Slowly Changing Dimension Wizard")  
  
## <a name="updating-slowly-changing-dimension-outputs"></a>更新渐变维度输出  
 更新渐变维度转换输出配置的最简单方法就是重新运行渐变维度向导并从向导页修改属性。 也可以使用 **“高级编辑器”** 对话框或以编程方式更新渐变维度转换。  
  
## <a name="see-also"></a>请参阅  
 [渐变维度转换](slowly-changing-dimension-transformation.md)  
  
  
