---
title: 渐变维度转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ef0312076baa49f264baba5fbd3eaf24bce8a47
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725873"
---
# <a name="slowly-changing-dimension-transformation"></a>渐变维度转换

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  渐变维度转换协调数据仓库维度表中的记录更新与插入。 例如，可以用此转换配置转换输出，这些转换输出使用来自 AdventureWorks OLTP 数据库中的 Production.Products 表的数据在 [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] 数据库的 DimProduct 表中插入和更新记录。  
  
> [!IMPORTANT]  
>  渐变维度向导仅支持与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的连接。  
  
 渐变维度转换提供用于管理渐变维度的以下功能：  
  
-   将传入行与查找表中的行匹配，以标识新行和现有行。  
  
-   在不允许更改时标识含有更改的传入行。  
  
-   标识需要更新的推断成员记录。  
  
-   标识包含需要插入新记录和更新过期记录的历史更改的传入行。  
  
-   检测包含需要更新现有记录（包括过期记录）的更改的传入行。  
  
 渐变维度转换支持四种类型的更改：变化的属性、历史属性、固定的属性和推断成员。  
  
-   变化的属性更改覆盖现有记录。 此类更改等效于类型 1 更改。 渐变维度转换将这些行定向到名为 **“变化的属性更新输出”** 的输出。  
  
-   历史属性更改创建新记录而不更新现有记录。 现有记录中允许的唯一更改是对指示记录是当前记录还是过期记录的列的更新。 此类更改等效于类型 2 更改。 渐变维度转换将这些行定向到两个输出：“历史属性插入输出”和“新输出”。  
  
-   固定的属性更改指示不得更改列值。 渐变维度转换检测更改，并可将带有更改的行定向到名为 **“固定的属性输出”** 的输出。  
  
-   推断成员指示该行是维度表中的推断成员记录。 当事实数据表引用尚未加载的维度成员时会存在推断成员。 按预期的相关维度数据（在维度数据的后续加载中提供）创建最小推断成员记录。 渐变维度转换将这些行定向到名为 **“推断成员更新”** 的输出。 当加载推断成员的数据后，可以更新现有记录，而不必创建一个新记录。  
  
> [!NOTE]  
>  渐变维度转换不支持类型 3 更改，该类型要求更改维度表。 通过标识具有固定的属性更新类型的列，可以捕获作为类型 3 更改候选项的数据值。  
  
 在运行时，渐变维度转换首先尝试将传入行与查找表中的记录匹配。 如果找不到匹配项，则传入行是一条新记录；因此渐变维度转换将不再执行其他工作，而是将传入行定向到 **“新输出”**。  
  
 如果找到匹配项，渐变维度转换检测传入行是否包含更改。 如果该行包含更改，渐变维度转换标识每列的更新类型，并将该行定向到 **“变化的属性更新输出”**、 **“固定的属性输出”**、 **“历史属性插入输出”** 或 **“推断成员更新输出”**。 如果该行未更改，渐变维度转换会将其定向到 **“不变的输出”**。  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>渐变维度转换输出  
 渐变维度转换有一个输入和最多六个输出。 输出将行定向到与该行的更新和插入要求相对应的数据流的子集。 此转换不支持错误输出。  
  
 下表介绍转换输出和这些输出的后续数据流的要求。 这些要求介绍渐变维度向导创建的数据流。  
  
|“输出”|描述|数据流要求|  
|------------|-----------------|----------------------------|  
|**“变化的属性更新输出”**|查找表中的记录被更新。 此输出用于变化的属性行。|OLE DB 命令转换使用 UPDATE 语句更新记录。|  
|**“固定的属性输出”**|不得更改的行中的值与查找表中的值不匹配。 此输出用于固定的属性行。|没有创建默认数据流。 如果转换配置为遇到固定的属性列更改时继续，则应创建可捕获这些行的数据流。|  
|**“历史属性插入输出”**|查找表至少包含一个匹配行。 标记为“当前”的行现在必须标记为“过期”。 此输出用于历史属性行。|派生列转换为过期行和当前行指示器创建列。 OLE DB 命令转换会更新现在必须标记为“过期”的记录。 具有新列值的行将定向到“新输出”，将在此处插入该行并标记为“当前”。|  
|**“推断成员更新输出”**|插入推断维度成员的行。 此输出用于推断成员行。|OLE DB 命令转换使用 SQL UPDATE 语句更新记录。|  
|**“新输出”**|查找表不包含匹配行。 将行添加到维度表中。 此输出用于新行和对历史属性行的更改。|派生列转换设置当前行指示器，而 OLE DB 目标则插入该行。|  
|**“不变的输出”**|查找表中的值与行值匹配。 此输出用于不变的行。|因为渐变维度转换未执行任何操作，所以没有创建默认数据流。 如果要捕获这些行，则应为此输出创建数据流。|  
  
## <a name="business-keys"></a>业务键  
 渐变维度转换至少需要一个业务键列。  
  
 渐变维度转换不支持空业务键。 如果数据中包含业务键列为空的行，则应从数据流中删除这些行。 可使用有条件拆分转换筛选业务键列中包含空值的行。 有关详细信息，请参阅 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>优化“渐变维度”转换的性能  
 有关如何提高渐变维度转换性能的建议，请参阅 [数据流性能特点](../../../integration-services/data-flow/data-flow-performance-features.md)。  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>渐变维度转换故障排除  
 您可以记录“渐变维度”转换对外部数据访问接口所做的调用。 利用此日志记录功能，可以排除“渐变维度”转换执行的对外部数据源的连接、命令和查询中发生的故障。 若要记录“渐变维度”转换对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>配置渐变维度转换  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>配置渐变维度转换输出  
 协调维度表中记录的更新和插入可以是一项复杂的任务，尤其是在同时使用了类型 1 和类型 2 更改的情况下。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器为配置对渐变维度的支持提供了以下两种方式：  
  
-   **“高级编辑器”** 对话框，在其中可以选择连接，设置公共组件属性和自定义组件属性，选择输入列，以及设置六个输出上的列属性。 若要完成为渐变维度配置支持的任务，必须为渐变维度转换所使用的输出手动创建数据流。 有关详细信息，请参阅 [Data Flow](../../../integration-services/data-flow/data-flow.md)。  
  
-   加载维度向导，指导您完成配置渐变维度转换以及为转换输出生成数据流的步骤。 若要更改渐变维度的配置，请重新运行加载维度向导。 有关详细信息，请参阅 [使用渐变维度向导配置输出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
  
-   blogs.msdn.com 上的博客文章 [优化渐变维度向导](https://go.microsoft.com/fwlink/?LinkId=199481)。  
  
  
