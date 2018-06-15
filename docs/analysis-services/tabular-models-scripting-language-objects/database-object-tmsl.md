---
title: 数据库对象 (TMSL) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9da6d97236811aaa0ef8ee757c7b2773bdda496a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045931"
---
# <a name="database-object-tmsl"></a>数据库对象 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  定义表格数据库兼容级别 1200年或更高版本，基于相同级别的模型。 本主题介绍了数据库，提供负载的请求的创建、 alter、 删除和执行数据库管理任务的对象定义。  
  
> [!NOTE]  
>  在任何脚本中，可以引用次只有一个数据库。 对于数据库本身之外的任何对象，数据库属性是可选如果你指定的模型。 没有模型可以用于推导的数据库名称，如果未显式提供的数据库之间的一对一映射。   
> 同样，您可以忽略模型，在数据库上设置其属性。  
  
## <a name="object-definition"></a>对象定义  
 所有对象都有一组通用的属性，包括名称、 类型、 说明、 一个属性集合和批注。 **数据库**对象还具有以下属性。  
  
 compatibilitylevel  
 目前，有效值为 1200，1400年。 较低的兼容性级别使用不同的元数据引擎。  
  
 readwritemode  
 枚举数据库的模式。 很常见，使数据库在高可用性或可伸缩性配置中以只读的。 有效的值包括 readWrite，  
                只读数组，  
                或 readOnlyExclusive。 请参阅[高可用性和 Analysis Services 中的可伸缩性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)和[切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)有关时使用此属性的详细信息。  
  
## <a name="usage"></a>用法  
 **数据库**中几乎每个命令使用对象。 请参阅[中表格模型脚本语言命令&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)有关的列表。 A**数据库**对象是某个服务器对象的子级。  
  
 在创建时，替换或更改数据库的对象，将指定对象定义的所有读写的属性。 省略一个读 / 写属性被视为删除操作。  
  
## <a name="partial-syntax"></a>部分语法  
 因为很大，此对象定义，则仅直接属性列。 **模型**对象提供的数据库定义大容量。 请参阅[模型对象&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)到的对象定义的方法。  
  
```  
    "database": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "type": "string"  
        },  
        "id": {  
          "type": "string"  
        },  
        "description": {  
          "type": "string"  
        },  
        "compatibilityLevel": {  
          "type": "integer"  
        },  
        "readWriteMode": {  
          "enum": [  
            "readWrite",  
            "readOnly",  
            "readOnlyExclusive"  
          ]  
        },  
        "model": {  
          "type": "object",  
          ...  
        }  
    }  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [高可用性和 Analysis Services 中的可伸缩性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)  
  
  
