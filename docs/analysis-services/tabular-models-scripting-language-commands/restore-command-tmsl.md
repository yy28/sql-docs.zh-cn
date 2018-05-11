---
title: 还原命令 (TMSL) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf99c62a4d50f29bb9fe9fbc57eebda45ff9be5e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="restore-command-tmsl"></a>还原命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  从备份文件还原 Analysis Services 数据库。  
  
## <a name="request"></a>请求  
  
```  
    {  
"restore": {  
            "description": "Parameters of Restore command of Analysis Services JSON API",  
            "properties": {  
            "database": {  
                "type": "string"  
            },  
            "file": {  
                "type": "string"  
            },  
            "password": {  
                "type": "string"  
            },  
            "dbStorageLocation": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type":boolean  
            },  
            "readWriteMode": {  
                "enum": [  
                "readWrite",  
                "readOnly",  
                "readOnlyExclusive"  
                ]  
. . .   
```  
  
 **还原**具有多个属性。  
  
||||  
|-|-|-|  
|**属性**|**默认**|**Description**|  
|database|[必需]|要还原的数据库对象的名称。|  
|文件|[必需]|备份文件名称/路径。|  
|password|Empty|用于解密备份的文件使用的密码。|  
|allowOverwrite|False|一个布尔值，如果为 true，指示已存在的备份文件将被覆盖;否则为 false。|  
|readWriteMode|ReadWrite|一个枚举值，该值指示允许对数据库的访问模式。<br /><br /> **枚举值如下所示：**<br /><br /> 允许 readWrite – 读写访问。<br /><br /> readOnly – 允许只读访问。<br /><br /> 允许 readOnlyExclusive – 只读独占访问。|  
|dbStorageLocation|Empty|还原的数据库的存储位置。|  
  
## <a name="response"></a>响应  
 如果该命令成功，则，返回空结果。 否则，返回 XMLA 异常。  
  
## <a name="example"></a>示例  
 **示例 1** -从本地文件夹中还原数据库。  
  
```  
{   
   "restore": {   
      "database":"AdventureWorksDW2014",  
      "file":"c:\\awdbdwfile.abf",  
      "security":"...",  
      "allowOverwrite":"true",  
      "password":"..",  
      "locations":"d:\\SQL Server Analysis Services\\data\\",  
      "storageLocation":".."  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>使用情况 （终结点）  
 语句中使用此命令元素[执行方法&#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)通过以下方式公开的 XMLA 终结点调用：  
  
-   作为 XMLA 窗口中 SQL Server Management Studio (SSMS)  
  
-   为输入文件到**调用 ascmd** PowerShell cmdlet  
  
-   输入到的 SSIS 任务或 SQL Server 代理作业  
  
 通过单击还原对话框上的脚本按钮，可以从 SSMS 生成用于此命令的现成脚本。  
  
 [ \[MS SSAS T\]: QL Server Analysis Services 表格 （SQL Server 技术协议）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文档包括部分 3.1.5.2.2，用于描述 JSON 表格元数据命令和对象的结构。 目前，该文档介绍命令和在 TMSL 脚本中尚未实现的功能。 请参阅主题[表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)阐述上支持的功能  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
