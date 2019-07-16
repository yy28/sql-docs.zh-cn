---
title: 开始使用 SSMA for Sybase 控制台 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bad08c06028a64a0423135b15641ebf6fa4e895e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029109"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>开始使用 SSMA for Sybase 控制台 (SybaseToSQL)
本部分介绍启动并开始使用 SSMA for Sybase 控制台应用程序的过程。 此处还列出了所使用的约定在典型的 SSMA 控制台输出窗口中。  
  
## <a name="launching-the-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤启动 SSMA 控制台应用程序：  
  
1.  转到开始，，然后指向所有程序。  
  
2.  单击**SQL Server Migration Assistant Sybase 命令提示符下**快捷方式。  
  
    它将显示 SSMA 控制台使用情况菜单和`(/? Help)`，以帮助你开始使用控制台应用程序。  
  
## <a name="using-the-ssma-console"></a>使用 SSMA 控制台  
在 Windows 系统上成功启动控制台后，可以使用以下步骤才能使用它：  
  
1.  通过脚本文件配置 SSMA 控制台。 本部分的详细信息，请参阅[创建脚本文件&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)。  
  
2.  [创建变量值文件&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [创建服务器连接文件&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [执行 SSMA 控制台&#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)根据您的项目需求。 
  
其他功能：  
  
1.  [指定一个密码](managing-passwords-sybasetosql.md)和导出/导入它到窗口的其他计算机。  
  
2.  [生成报告](generating-reports-sybasetosql.md)若要查看详细的 xml 输出为评估/转换和数据迁移的报告。 此外可以生成刷新和同步命令的详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
执行 SSMA 脚本命令和选项，在控制台程序为用户在控制台上显示的结果和消息 （信息、 错误等） 或者，如有必要，将重定向到的 xml 输出文件。 每种类型的输出中的消息是由唯一的颜色表示。 例如，白色颜色中的文本消息表示文件的脚本命令;以绿色表示一个表示提示用户输入，依此类推。  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
下表中将显示控制台输出的颜色的解释：  
  
|颜色|描述|  
|---------|---------------|  
|Red|执行期间出错|  
|灰色|日期和时间戳，向用户显示消息|  
|白色|脚本文件命令、 消息类型|  
|Yellow|警告|  
|绿色|提示用户输入|  
|蓝绿色|开始、 完成和操作的结果|  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
