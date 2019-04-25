---
title: 开始使用 SSMA for Access 控制台 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 44e89e7c6ab10df13927247222e1f8564500fb8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62759879"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>开始使用 SSMA for Access 控制台 (AccessToSQL)
本部分介绍的过程启动并开始使用访问控制台应用程序。 此外列出，本文所述，将使用的约定在典型的 SSMA 控制台输出窗口中。  
  
## <a name="launching-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤启动 SSMA 控制台应用程序：  
  
1.  转到**启动**，然后指向**所有程序**。  
  
2.  单击**SQL Server Migration Assistant 用于访问命令提示符**快捷方式。  
  
    它将显示 SSMA 控制台使用情况菜单和`(/? Help)`，以帮助你开始使用控制台应用程序。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 控制台的过程  
在 Windows 系统上成功启动控制台之后，可以使用以下步骤才能使用它：  
  
1.  通过脚本文件配置 SSMA 控制台。 本部分的详细信息，请参阅[创建脚本文件&#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)。  
  
2.  [创建变量值文件&#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [创建服务器连接文件&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [执行 SSMA 控制台&#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md)根据您的项目需求  
  
其他功能：  
  
1.  [指定一个密码](managing-passwords-accesstosql.md)和导出 / 导入到其他窗口机  
  
2.  [生成报告](generating-reports-accesstosql.md)若要查看详细的 xml 输出为评估 /conversion 和数据迁移的报告。 此外可以刷新和同步命令的生成详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
执行 SSMA 脚本命令和选项，时控制台程序为用户在控制台上显示的结果和消息 （信息、 错误等），或如有必要，将重定向到的 xml 输出文件。 每种类型的输出中的消息是由唯一的颜色表示。 例如，白色颜色中的文本消息表示文件的脚本命令;以绿色表示一个表示提示用户输入，依此类推。  
  
![SSMA 控制台输出](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA 控制台输出")  
  
下表中的控制台输出的颜色解释：  
  
|颜色|Description|  
|---------|---------------|  
|Red|执行期间出错|  
|灰色|日期和时间戳，向用户显示消息|  
|白色|脚本文件命令、 消息类型|  
|Yellow|警告|  
|绿色|提示用户输入|  
|蓝绿色|开始、 完成和操作的结果|  
  
## <a name="see-also"></a>请参阅  
[安装用于访问 SQL Server 迁移助手](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
