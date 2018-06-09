---
title: 入门 MySQL 控制台 (MySQLToSQL) SSMA |Microsoft 文档
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
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
caps.latest.revision: 23
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 75e189d89c9a1bbc7207521b8156d0f4b56ca759
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776233"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>Getting Started with SSMA MySQL 控制台 (MySQLToSQL)
本部分介绍的过程启动并开始使用 MySQL 控制台应用程序。 此外列出，本文所述，将使用的约定在典型的 SSMA 控制台输出窗口。  
  
## <a name="launching-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤来启动 SSMA 控制台应用程序：  
  
1.  转到**启动**和指向**所有程序**。  
  
2.  单击**SQL Server Migration Assistant 有关 MySQL 命令提示符**快捷方式。  
  
    它显示的 SSMA 控制台使用情况菜单和`(/? Help)`，来帮助你开始使用控制台应用程序。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 控制台的过程  
在 Windows 系统上成功启动控制台之后，你可以使用以下步骤才能使用它：  
  
1.  通过脚本文件配置 SSMA 控制台。 本部分的详细信息，请参阅[创建脚本文件&#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md) 。  
  
2.  [创建变量值文件&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [创建服务器连接文件&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [执行 SSMA 控制台&#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)基于您的项目需求  
  
其他功能：  
  
1.  [保护密码](http://msdn.microsoft.com/en-us/4ffbc587-ea3f-49ad-bc42-a654f672325e)和导出 / 导入到其他窗口机  
  
2.  [生成报表](http://msdn.microsoft.com/en-us/1c0202e8-546d-4cb3-a37f-1d2e35d53839)以查看详细的 xml 输出评估 /conversion 和数据迁移的报表。 此外可以刷新和同步命令生成详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
时执行的 SSMA 脚本命令和选项，控制台程序为用户在控制台上显示的结果和消息 （信息、 错误等），或如果需要，重定向到 xml 输出文件。 每种类型的输出中的消息是由唯一的颜色表示。 例如，白色的颜色的颜色的文本消息表示脚本文件命令;绿色中的一个表示提示用户输入，依次类推。  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
下表中的控制台输出的颜色解释：  
  
|Color|Description|  
|---------|---------------|  
|Red|在执行期间的错误|  
|灰色|日期和时间戳，向用户显示消息|  
|白色|脚本文件命令，消息类型|  
|Yellow|警告|  
|绿色|提示用户输入|  
|青色|启动，完成和操作的结果|  
  
## <a name="see-also"></a>请参阅  
[安装适用于 MySQL SSMA](http://msdn.microsoft.com/en-us/e89b45bd-59c1-4d23-8bd7-3dafc1947448)  
  
