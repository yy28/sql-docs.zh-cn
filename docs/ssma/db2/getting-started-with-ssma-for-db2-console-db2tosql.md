---
title: 开始使用 SSMA for DB2 控制台 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f245c017-023e-4880-8721-8908d339525e
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c74c3f21508ce08e6e540dd5c4cc84531b7c744d
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392695"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>开始使用 SSMA for DB2 控制台 (DB2ToSQL)
本部分介绍的过程启动并开始使用 DB2 控制台应用程序。 此外列出，本文所述，将使用的约定在典型的 SSMA 控制台输出窗口中。  
  
## <a name="launching-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤启动 SSMA 控制台应用程序：  
  
1.  转到**启动**，然后指向**所有程序**。  
  
2.  单击 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant 用于 DB2 的命令提示符**快捷方式。  
  
    它将显示 SSMA 控制台使用情况菜单和`(/? Help)`，以帮助你开始使用控制台应用程序。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 控制台的过程  
在 Windows 系统上成功启动控制台之后，可以使用以下步骤才能使用它：  
  
1.  通过脚本文件配置 SSMA 控制台。 本部分的详细信息，请参阅[创建脚本文件&#40;DB2ToSQL&#41; ](../../ssma/db2/creating-script-files-db2tosql.md) 。  
  
2.  [创建变量值文件&#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [创建服务器连接文件&#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [执行 SSMA 控制台&#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md)根据您的项目需求  
  
其他功能：  
  
1.  [管理密码](http://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94)和导出 / 导入到其他窗口机  
  
2.  [生成报告](http://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883)若要查看详细的 xml 输出为评估 /conversion 和数据迁移的报告。 此外可以刷新和同步命令的生成详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
执行 SSMA 脚本命令和选项，时控制台程序为用户在控制台上显示的结果和消息 （信息、 错误等），或如有必要，将重定向到的 xml 输出文件。 每种类型的输出中的消息是由唯一的颜色表示。 例如，白色颜色中的文本消息表示文件的脚本命令;以绿色表示一个表示提示用户输入，依此类推。  
  
![Ssmaconsoleoutput_oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "ssmaconsoleoutput_oracle")  
  
下表中的控制台输出的颜色解释：  
  
|Color|Description|  
|---------|---------------|  
|Red|执行期间出错|  
|灰色|日期和时间戳，向用户显示消息|  
|白色|脚本文件命令、 消息类型|  
|Yellow|警告|  
|绿色|提示用户输入|  
|蓝绿色|开始、 完成和操作的结果|  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for DB2](http://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
