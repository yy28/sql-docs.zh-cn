---
title: DMX 模板 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bf7682ce42422efb0e47e4272e53933eba92a4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081562"
---
# <a name="dmx-templates"></a>DMX 模板
  数据挖掘模板可帮助您快速生成复杂的查询。 虽然 DMX 查询的常规语法具有详细说明，但借助于这些模板，可通过单击并且指向参数和数据源，更轻松地生成查询。  
  
## <a name="using-the-templates"></a>使用模板  
  
1.  在 Excel 数据挖掘客户端中，单击 "**查询**"。  
  
2.  在向导的 "**开始**" 页上，单击 "**下一步**"。  
  
3.  在该页上，**选择 "模型**"，然后单击 "**高级**"。  
  
     **提示：** 如果要在模型中创建预测查询，则可以先选择该模型，然后单击 "**高级**"，使用模型名称预填充模板。  
  
4.  在 "**数据挖掘高级查询编辑器**" 中，单击 " **DMX 模板**"，然后选择一个模板。  
  
5.  按 Enter 将模板加载到“DMX 查询”窗格中。  
  
6.  继续单击模板中的链接，在对话框出现后，选择相应的输出、模型或参数。  
  
     对于预测查询，请首先选择输入数据集，然后映射列。  
  
7.  单击 "**编辑查询**" 以切换到文本编辑器视图，并手动更改查询。  
  
     但要注意，如果在使用查询编辑器时切换视图，则上一视图中的所有信息都将被清除。 更改视图前，请将 DMX 语句复制并粘贴到一个单独的文件中，保存好您的工作结果。  
  
8.  单击“完成”  。 在 "**选择目标**" 对话框中，指定要将结果保存到的位置。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  如果成功执行语句，则发送到服务器的 DMX 语句也将记录在**跟踪**窗口中。 有关如何使用跟踪功能的详细信息，请参阅[trace &#40;Excel 数据挖掘客户端&#41;](trace-data-mining-client-for-excel.md)。  
  
 有关如何使用 "数据挖掘高级查询编辑器" 的详细信息，请参阅[查询 &#40;SQL Server 数据挖掘外接程序 "&#41;](query-sql-server-data-mining-add-ins.md)和[高级数据挖掘查询编辑器](advanced-data-mining-query-editor.md)。  
  
## <a name="list-of-dmx-templates"></a>DMX 模板的列表  
 以下 DMX 模板包含在 Excel 数据挖掘客户端中。  
  
 **预测**  
  
 使用这些模板可创建高级预测查询，包括外接程序中向导不支持的查询，例如使用嵌套表或外部数据源的查询。  
  
-   筛选的预测  
  
-   筛选的嵌套预测  
  
-   嵌套的预测  
  
-   单独预测  
  
-   标准预测  
  
-   时序预测  
  
-   TOP 预测查询  
  
-   嵌套表的 TOP 预测查询  
  
 **创建**  
  
 使用这些模板可生成自定义模型或数据结构。 您不仅限于向导支持的模型，您可以使用您连接到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的实例所支持的任何数据挖掘算法，包括插件算法。  
  
-   挖掘模型  
  
-   挖掘结构  
  
-   具有维持的挖掘结构  
  
-   临时模型  
  
-   临时结构  
  
 **模型属性**  
  
 使用这些模板可创建获取有关模型和定型集的元数据的查询。 还可以从模型内容中检索详细信息，或者获取定型数据的统计配置文件。  
  
-   挖掘模型内容  
  
-   最小和最大列值  
  
-   挖掘结构测试/定型事例  
  
-   离散列值  
  
 **管理**  
  
 使用这些模板可执行 DMX 支持的任何管理任务，包括导入和导出模型、删除模型以及清除模型或数据结构。  
  
-   清除挖掘模型  
  
-   清除结构和模型  
  
-   清除挖掘结构  
  
-   删除挖掘模型  
  
-   删除挖掘结构  
  
-   重命名挖掘模型  
  
-   重命名挖掘结构  
  
-   为挖掘模型定型  
  
-   为嵌套挖掘结构定型  
  
-   为挖掘结构定型  
  
### <a name="requirements"></a>要求  
 根据使用的模板，您可能需要具有管理权限才能访问 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器和执行查询。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)  
  
  
