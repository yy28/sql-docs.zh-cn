---
title: 同步命令 (TMSL) |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4265e6fa1e2214fae53cacdb084e152005eb3647
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033270"
---
# <a name="synchronize-command-tmsl"></a>同步命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  利用另一个现有数据库同步 Analysis Services 数据库。  
  
## <a name="request"></a>请求  
 属性接受 JSON 的 synchronize 命令如下所示。  
  
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
  
 属性接受 JSON 的 synchronize 命令如下所示。  
  
||||  
|-|-|-|  
|**属性**|**Default**|**Description**|  
|“数据库”||要同步的数据库对象的名称。|  
|源 (source)||要用于连接到源服务器的连接字符串。|  
|synchronizeSecurity|skipMembership|一个枚举值，指定如何还原安全定义，包括角色和权限。 有效值包括 skipMembership、 copyAll、 ignoreSecurity。|  
|applyCompression|True|一个布尔值，如果为 true，表示将在同步操作; 期间应用压缩否则为 false。|  
  
## <a name="response"></a>响应  
 如果命令成功，则返回空结果。 否则，返回了 XMLA 异常。  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 在一条语句中使用此命令元素[执行的方法&#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点的调用：  
  
-   为 SQL Server Management Studio (SSMS) 中的 XMLA 窗口  
  
-   作为对输入文件**调用 ascmd** PowerShell cmdlet  
  
-   为 SSIS 任务或 SQL Server 代理作业的输入  
  
 通过单击同步数据库对话框上的脚本按钮，可以从 SSMS 生成用于此命令的现成脚本。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍了命令和 TMSL 脚本中尚未实现的功能。 请参阅主题[表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)获取有关支持功能的  
  
## <a name="see-also"></a>请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
