---
title: "用于访问控制台 (AccessToSQL) 入门 SSMA |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2b555cebf6fbfda157b72e8bc71b10600da54d39
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>用于访问控制台 (AccessToSQL) 入门 SSMA
本部分介绍的过程启动并开始使用访问控制台应用程序。 此外列出，本文所述，将使用的约定在典型的 SSMA 控制台输出窗口。  
  
## <a name="launching-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤来启动 SSMA 控制台应用程序：  
  
1.  转到**启动**和指向**所有程序**。  
  
2.  单击**SQL Server Migration Assistant 的访问的命令提示符**快捷方式。  
  
    它显示的 SSMA 控制台使用情况菜单和`(/? Help)`，来帮助你开始使用控制台应用程序。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 控制台的过程  
在 Windows 系统上成功启动控制台之后，你可以使用以下步骤才能使用它：  
  
1.  通过脚本文件配置 SSMA 控制台。 本部分的详细信息，请参阅[创建脚本文件 &#40;AccessToSQL &#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [创建变量的值文件 &#40;AccessToSQL &#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [创建服务器连接文件 &#40;AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [执行 SSMA 控制台 &#40;AccessToSQL &#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)基于您的项目需求  
  
其他功能：  
  
1.  [指定密码](http://msdn.microsoft.com/en-us/b099d0f9-dd37-4c87-8b6f-ed0177881ea4)和导出 / 导入到其他窗口机  
  
2.  [生成报表](http://msdn.microsoft.com/en-us/abb4264a-622e-4215-af5b-14e309b8a399)以查看详细的 xml 输出评估 /conversion 和数据迁移的报表。 此外可以刷新和同步命令生成详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
时执行的 SSMA 脚本命令和选项，控制台程序为用户在控制台上显示的结果和消息 （信息、 错误等），或如果需要，重定向到 xml 输出文件。 每种类型的输出中的消息是由唯一的颜色表示。 例如，白色的颜色的颜色的文本消息表示脚本文件命令;绿色中的一个表示提示用户输入，依次类推。  
  
![SSMA 控制台输出](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA 控制台输出")  
  
下表中的控制台输出的颜色解释：  
  
|Color|Description|  
|---------|---------------|  
|Red|在执行期间的错误|  
|灰色|日期和时间戳，向用户显示消息|  
|白色|脚本文件命令，消息类型|  
|Yellow|警告|  
|绿色|提示用户输入|  
|青色|启动，完成和操作的结果|  
  
## <a name="see-also"></a>另请参阅  
[安装访问的 SQL Server 迁移的助手](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)  
  

