---
title: "序列命令 (TMSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/12/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 898d6ec2-9b40-441b-be2b-5728d1d2882e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d1c5a1108ca775694122b6e9c5518913b47d85aa
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="sequence-command-tmsl"></a>Sequence 命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  使用**序列**命令来运行一组连续的操作在批处理模式下的 Analysis Services 实例上。  整个命令和所有其组成部分必须完成事务后，若要成功执行顺序。  
  
 可以运行以下命令除外的按顺序，**刷新**并行同时处理多个对象运行的命令。  
  
-   [创建命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)  
  
-   [CreateOrReplace 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)  
  
-   [Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)  
  
-   [删除命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)  
  
-   [刷新命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)  
  
-   [备份命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)  
  
-   [还原命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)  
  
-   [附加命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)  
  
-   [Detach 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)  
  
## <a name="request"></a>请求  
 **maxParallelism**是一个可选属性，它确定是否**刷新**按顺序或并行运行的操作。  
  
 默认行为是尽可能使用尽可能并行度。 通过将嵌入**刷新**内**序列**，你可以控制在处理期间，包括限制到仅在一个线程的操作使用的线程的精确数目。  
  
> [!NOTE]  
>  分配给整数**maxParallelism**确定最大处理期间使用的线程数。 有效值为任意正整数。 将该值设置为 1 等于不并行 （使用一个线程）。  
  
 仅**刷新**并行运行。 如果你修改**maxParallelism**若要使用固定的数目的线程，请务必查看属性，在[刷新命令&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)以了解的潜在影响。 就可能会破坏并行度，即使已设为多个线程可用的方式设置属性。 刷新类型按下列顺序将为你提供最佳并行度：  
  
-   首先，为使用 ClearValues 的所有对象指定刷新  
  
-   接下来，为使用 DataOnly 的所有对象指定刷新  
  
-   上次为使用完整、 计算、 自动或添加的所有对象指定刷新  
  
 任何变体这将中断并行度。  
  
```  
{   
  "sequence":    
    {   
      "maxParallelism": 3,   
      "operations": [   
        {   
          "mergepartitions": {   
            "sources": [   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition1"   
              },   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition2"   
              }   
            ]   
          }   
        },   
        {   
          "refresh": {   
            "type": "calculate",   
            "objects": {   
             "database": "salesdatabase"   
            }   
          }   
        }   
      ]   
    }      
}   
```  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法&#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 无法从 SSMS 生成用于此命令的现成脚本。 相反，你可以从一个示例开始或编写自己。  
  
 [ \[MS SSAS T\]: SQL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构. 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题 ([表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 阐述上支持的功能。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
