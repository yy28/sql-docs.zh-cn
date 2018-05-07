---
title: 用于 Oracle 控制台 (OracleToSQL) 入门 SSMA |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 95da4265bcaf56f7abbd5e445d93760790752b22
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>用于 Oracle 控制台 (OracleToSQL) 入门 SSMA
本部分介绍的过程启动并开始使用 Oracle 控制台应用程序。 此外列出，本文所述，将使用的约定在典型的 SSMA 控制台输出窗口。  
  
## <a name="launching-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤来启动 SSMA 控制台应用程序：  
  
1.  转到**启动**和指向**所有程序**。  
  
2.  单击**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]迁移助手的 Oracle 命令提示符**快捷方式。  
  
    它显示的 SSMA 控制台使用情况菜单和`(/? Help)`，来帮助你开始使用控制台应用程序。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 控制台的过程  
在 Windows 系统上成功启动控制台之后，你可以使用以下步骤才能使用它：  
  
1.  通过脚本文件配置 SSMA 控制台。 本部分的详细信息，请参阅[创建脚本文件&#40;OracleToSQL&#41; ](../../ssma/oracle/creating-script-files-oracletosql.md) 。  
  
2.  [创建变量值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [创建服务器连接文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [执行 SSMA 控制台&#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)基于您的项目需求  
  
其他功能：  
  
1.  [指定密码](http://msdn.microsoft.com/en-us/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c)和导出 / 导入到其他窗口机  
  
2.  [生成报表](http://msdn.microsoft.com/en-us/ccad6262-01e1-447a-bd2b-c105154c80ce)以查看详细的 xml 输出评估 /conversion 和数据迁移的报表。 此外可以刷新和同步命令生成详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
时执行的 SSMA 脚本命令和选项，控制台程序为用户在控制台上显示的结果和消息 （信息、 错误等），或如果需要，重定向到 xml 输出文件。 每种类型的输出中的消息是由唯一的颜色表示。 例如，白色的颜色的颜色的文本消息表示脚本文件命令;绿色中的一个表示提示用户输入，依次类推。  
  
![Ssmaconsoleoutput_oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "ssmaconsoleoutput_oracle")  
  
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
[安装适用于 Oracle SSMA](http://msdn.microsoft.com/en-us/9211013a-ab24-4c52-9b26-87994b35e502)  
  
