---
title: "Synchronize 命令 (TMSL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: a32ff053-f38f-49d7-afdc-e19f59c88135
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6912b3c73f898335853ff3ffe78021fad75bb357
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="synchronize-command-tmsl"></a>Synchronize 命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  利用另一个现有数据库同步 Analysis Services 数据库。  
  
## <a name="request"></a>请求  
 接受的 JSON 属性的 synchronize 命令如下所示。  
  
```  
{   
   "synchronize":{   
      "database":"AdventureWorksDW_Production",  
      "source":"Provider=MSOLAP.7;Data Source=localhost;Integrated Security=SSPI;Initial Catalog=AdventureWorksDW_Dev",  
      "synchronizeSecurity":"copyAll",  
      "applyCompression":true  
   }  
}  
```  
  
 接受的 JSON 属性的 synchronize 命令如下所示。  
  
||||  
|-|-|-|  
|**属性**|**Default**|**Description**|  
|database||要同步的数据库对象的名称。|  
|源 (source)||要用于连接到源服务器的连接字符串。|  
|synchronizeSecurity|skipMembership|一个枚举值，指定如何还原安全定义，包括角色和权限。 有效值包括 skipMembership、 copyAll、 ignoreSecurity。|  
|applyCompression|True|一个布尔值，如果为 true，指示将在同步操作; 期间应用压缩否则为 false。|  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 通过单击同步数据库对话框上的脚本按钮，可以从 SSMS 生成用于此命令的现成脚本。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题[表格模型脚本语言 &#40;TMSL &#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)阐述上支持的功能  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
