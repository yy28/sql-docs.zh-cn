---
title: 附加命令 (TMSL) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fcafff4ce1b5e87a9ca3e7933989ecbf9bf52bf3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039971"
---
# <a name="attach-command-tmsl"></a>附加命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  将 Analysis Services 文件附加到服务器。  
  
  
## <a name="request"></a>请求  
  
```  
{   
   "attach":{   
      "folder":"C:\\Program Files\\Microsoft SQL Server\\MSAS13.Tabular\\OLAP\\Data\\",  
      "readWriteMode":"readOnly",  
      "password":"secret"  
   }  
}  
```  
  
 接受的 JSON 属性附加命令如下所示。  
  
||||  
|-|-|-|  
|**属性**|**默认**|**Description**|  
|database|[必需]|要附加的数据库对象名称。|  
|文件夹|[必需]|包含附加的数据库的文件夹。|  
|password|Empty|要用于加密附加的数据库中的机密的密码。|  
|readWriteMode|ReadWrite|一个枚举值，该值指示允许对数据库的访问模式。<br /><br /> **枚举值如下所示：**<br /><br /> 允许 readWrite – 读写访问。<br /><br /> readOnly – 允许只读访问。<br /><br /> 允许 readOnlyExclusive – 只读独占访问。|  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法&#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 通过单击附加数据库对话框上的脚本按钮，可以从 SSMS 生成用于此命令的现成脚本。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题[表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)阐述上支持的功能  

## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [附加和分离 Analysis Services 数据库](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
