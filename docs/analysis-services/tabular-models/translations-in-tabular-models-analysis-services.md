---
title: "表格模型 (Analysis Services) 中的翻译 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e67f88f5-9f0c-4f19-ab09-558c56ca9335
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 28ff4ea7472597ae86b426ec0a15de399f56d14f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="translations-in-tabular-models-analysis-services"></a>表格模型 (Analysis Services) 中的翻译
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]将添加翻译字符串支持的表格模型。 该模型中的单个对象可以拥有多个名称或说明翻译，使其可以在模型定义中支持多种语言。  
  
 已翻译的字符串仅适用于出现在客户端工具（如 Excel 数据透视表列表）中的对象元数据（表和列的名称及说明）。  若要使用已翻译的字符串，客户端连接需指定区域性。 在“在 Excel 中分析”功能中，可以从下拉列表中选择语言。 对于其他工具，可能需要在连接字符串中指定区域性。  
  
 此功能不适用于将已翻译的数据加载到模型中。 如果希望加载已翻译的数据值，应制定一种处理策略，包括如何从提供数据的数据源提取已翻译的字符串。  
  
 添加已翻译元数据的典型工作流如下所示：  
  
-   生成空的翻译 JSON 文件，该文件应包含每个字符串翻译的占位符  
  
-   将字符串翻译添加到 JSON 文件  
  
-   将翻译导回模型中  
  
-   生成、处理或部署模型  
  
-   使用允许在连接字符串上使用 LCID 的客户端应用程序连接到模型  
  
## <a name="create-an-empty-translation-file"></a>创建一个空的翻译文件  
 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 添加翻译。  
  
1.  单击“模型” > “翻译” > “管理翻译”。  
  
2.  选择要为其提供翻译的语言，然后单击“添加” 。  
  
3.  从列表中选择一种或多种语言，具体取决于你希望导入字符串的方式。  
  
     虽然翻译文件可以包含多种语言，但是你可能会发现如果每种语言创建一个翻译文件，那么翻译管理就更容易。 稍后将会完全导入你现在创建的翻译文件。 若要根据语言改变导入选项，每种语言都需位于其自己的文件中。  
  
4.  单击“导出语言文件” 。  提供文件名和文件位置。  
  
 ![ssas-表格-转换-导出](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas-表格-转换-导出")  
  
## <a name="add-translations"></a>添加翻译  
 空的 JSON 翻译文件包括特定语言翻译的元数据。 在模型定义末尾的 **Culture** 部分指定了对象名称和说明的翻译占位符。 可为以下各项添加翻译：  
  
|||  
|-|-|  
|translatedCaption|出现在支持表格模型可视化的任何客户端应用程序中的表标题或列标题。|  
|translatedDescription|比标题少见，在建模工具（如 SSDT）中显示为模型信息的说明。|  
  
 不要从文件中删除任何未指定的元数据。  它应与其所基于的文件一致。 只需添加所需字符串，然后保存该文件。  
  
 虽然  **referenceCulture** 看起来像应该修改的内容，但它包含该模型默认区域性中的元数据。 导入期间将不会读入，并将忽略对 **referenceCulture** 部分所做的任何更改。  
  
 以下示例显示了 **DimProduct** 表和 **DimCustomer** 表的已翻译标题和说明。  
  
 ![ssas-表格-转换-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-表格-转换-json")  
  
> [!TIP]  
>  可以使用任何 JSON 编辑器打开文件，但是建议你使用 Visual Studio 中的 JSON 编辑器，以便你能使用解决方案资源管理器中的“查看代码”命令来查看 SSDT 中的表格模型定义。 若要获取 JSON 编辑器，需 [安装 Visual Studio 2015 的完整版本](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)。 免费的社区版包括 JSON 编辑器。  
  
## <a name="import-a-translation-file"></a>导入翻译文件  
 导入的翻译字符串会成为模型定义的永久部分。 导入这些字符串后，将不再引用翻译文件。  
  
1.  单击“模型” > “翻译” > “导入翻译”。  
  
2.  查找翻译文件，然后单击“打开” 。  
  
3.  根据需要指定导入选项。  
  
    |||  
    |-|-|  
    |覆盖现有翻译|导入文件的过程中，将替换同一语言的所有现有标题或说明。|  
    |忽略无效对象|指定应忽略元数据偏差还是标记为错误。|  
    |将导入结果写入日志文件|默认情况下，系统会将日志文件保存到项目文件夹。 导入结束后，系统将提供文件的确切路径。 日志文件名称是 SSDT_Translations_Log_\<时间戳 >。|  
    |导入前，将翻译备份到 JSON 文件|备份与要导入的字符串的区域性一致的现有翻译。  如果模型中不存在要导入的区域性，则备份将为空。<br /><br /> 如果以后需要还原此文件，可以将 model.bim 的内容替换为此 JSON 文件。|  
  
4.  单击“导入” 。  
  
5.  根据需要，如果已生成日志文件或备份，可以在项目文件夹（例如，C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW）中找到该文件。  
  
6.  若要验证导入，请执行以下步骤：  
  
    -   右键单击解决方案资源管理器中的“model.bim”文件，然后选择“查看代码”。 单击“是”以关闭设计视图，并在代码视图中重新打开“model.bim”。  如果已安装完整版的 Visual Studio（例如免费的社区版），则会在内置 JSON 编辑器中打开文件。  
  
    -   搜索“区域性”或特定的已翻译字符串，以验证希望看到的字符串实际存在。  
  
## <a name="connect-using-a-locale-identifier"></a>使用区域设置标识符进行连接  
 本部分介绍了一种用于验证是否已从模型中返回正确字符串的方法。  
  
1.  在 Excel 中，连接到表格模型。 此步骤假定已部署该模型。 如果该模型仅存在于工作区中，则将其部署到 Analysis Services 实例以完成验证检查。  
  
     或者，可以使用“在 Excel 中分析”  功能以连接到该模型  
  
2.  在 Excel 连接对话框中，为模型中存在的字符串翻译选择区域性。 Excel 检测模型中定义的区域性，并相应填充下拉列表。  
  
     ![ssas-表格的翻译的 excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-表格的翻译的 excel")  
  
     创建数据透视表时，将看到已翻译的表和列名称。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 的全球化方案](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [在 Excel 中分析（SSAS 表格）](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  

