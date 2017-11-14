---
title: "模型对象 (TMSL) |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9382d0d6-2d4b-49ad-a0eb-35970f0f3afb
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 369bf544360d50c061314f45c04e8fb55784184c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="model-object-tmsl"></a>模型对象 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  定义表格模型。 没有每个数据库，并只有一个数据库可以在任何给定的命令中指定的一个模型。 数据库对象是父对象。  
  
 模型定义来说太大，以重现一个主题中的整个语法。 为此，突出显示的主要部分的部分语法可下面，找到与链接到子对象。  
  
 可能是了解模型定义的最佳方法是从开始您所熟知的表格模型。 使用**查看代码**SQL Server Data Tools 中的选项以查看其定义。 请记住要安装 JSON 编辑器，以便你可以查看的代码。 你可以通过 Visual Studio 中获取 JSON 编辑器[下载 Community edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)或其他版本的 Visual Studio。  
  
> [!NOTE]  
>  在任何脚本中，可以引用次只有一个数据库。 对于数据库本身之外的任何对象，数据库属性是可选如果你指定的模型。 没有模型可以用于推导的数据库名称，如果未显式提供的数据库之间的一对一映射。   
> 同样，您可以忽略模型，在数据库上设置其属性。  
  
## <a name="object-definition"></a>对象定义  
 所有对象都有一组通用的属性，包括名称、 类型、 说明、 一个属性集合和批注。 **模型**对象还具有以下属性。  
  
 storageLocation  
 要放置模型磁盘上的位置。  
  
 defaultMode  
 为使数据在分区中可用的默认方法。  
  
 defaultDataView  
 对于在 DirectQuery 模式下的模型，此属性确定哪个分区用于对模型运行查询。  有效值包括完全安装选项和示例。  
  
 区域性  
 要用于设置格式的区域性。  
  
 collation  
 排序规则序列中。 请参阅[Analysis Services 的全球化方案](../../analysis-services/globalization-scenarios-for-analysis-services.md)有关详细信息。  
  
 表  
 在模型中，包括分区、 列、 度量值、 Kpi 和批注的表的完整集合。 请参阅[表对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)有关详细信息。  
  
 关系  
 指定每对表，包括设置筛选器方向和安全性的属性之间的关系。 请参阅[关系对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)有关详细信息。  
  
 数据源  
 通过查询传递到外部数据库向模型提供数据或用于的一个或多个连接。 请参阅[数据源对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)有关详细信息。  
  
 角色  
 将数据库权限、 成员帐户和 （可选） 在 DAX 中的自定义访问控制的安全筛选器关联的对象。  
  
## <a name="usage"></a>用法  
 **模型**对象包含整个模型。 你需要在大多数命令中指定一个模型和/或其父数据库对象。  
  
 在创建时，替换或更改模型的对象，将指定对象定义的所有读写的属性。 省略一个读 / 写属性被视为删除操作。  
  
## <a name="partial-syntax"></a>部分语法  
 由于此对象定义是很大，列出的第一个级别属性。 请参阅[对象定义中表格模型脚本语言 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)有关子对象的列表。  
  
```  
    "model": {  
      "description": "Model object of a Tabular database",  
      "type": "object",  
      "properties": {  
          "name": {  },  
          "description": {  },  
         "storageLocation": {  },  
         "defaultMode":  {  },  
         "defaultDataView": {  },  
         "culture": {  },  
         "collation": {  },  
         "annotations": {  },  
         "tables": {  },  
         "relationships": {  },  
         "dataSources": {  },  
         "perspectives": {  },  
            "cultures": {  },  
         "roles": {  }  
    }  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  

