---
title: SSMA 控制台 (AccessToSQL) 中的命令行选项 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 21775252d57184914d9c1d595ce5f8b67e8e4cbf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396071"
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>SSMA 控制台 (AccessToSQL) 中的命令行选项
Microsoft 为您提供了一套稳健的命令行选项来执行和控制 SSMA 活动。 下来的几节提供其他详细信息。  
  
## <a name="command-line-options-in-the-ssma-console"></a>SSMA 控制台中的命令行选项  
此处所述的控制台命令选项。  
  
为便于本部分中，术语 '选项也称为转换。  
  
选项不区分大小写，并且可能会启动与**-** 或**/** 字符。  
  
如果指定了选项，是必须指定相应的选项参数。  
  
由空白，必须从选项字符分隔选项参数。  
  
**语法示例：**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
包含空格的文件夹或文件名称应指定用双引号括起来。  
  
命令行条目和错误消息的输出存储在标准输出或指定文件中。  
  
### <a name="script-file-option-sscript"></a>编写的脚本文件选项:-s/脚本  
强制性开关，脚本文件路径/名称指定命令序列 SSMA 要执行该脚本。  
  
**语法示例：**  
  
`C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>变量值文件选项: – v/变量  
变量值文件包含脚本文件中使用的变量。 开关是可选的。 如果未在可变文件中声明变量和脚本文件中使用，应用程序将生成一个错误并终止控制台执行。  
  
**语法示例：**  
  
-   在多个变量值文件中，可能是一个具有默认值，另一个具有特定于实例的值在适用时定义的变量。 最后一个命令行参数中指定的变量文件采用首选项，以防止出现重复的变量：  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>服务器连接文件选项: – c/serverconnection  
此文件包含服务器的每个服务器的连接信息。 每个服务器定义标识的唯一服务器 id。 服务器 Id 与连接相关的命令的脚本文件中引用。  
  
服务器定义可以是服务器连接文件和/或脚本文件的一部分。 在脚本文件中的服务器 id 将优先于服务器连接文件，以防服务器 id 重复。  
  
**语法示例：**  
  
-   脚本文件中使用服务器 Id。 它们是单独的服务器连接文件中定义的。 此文件使用变量值文件中定义的变量：  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   服务器定义嵌入的脚本文件：  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 输出选项:-x / xmloutput [xmloutputfile]  
此命令用于将命令输出消息到控制台或 xml 文件以 xml 格式输出。  
  
有两个选项可用于 xmloutput，即：  
  
-   如果文件路径提供 xmloutput 切换后，输出是重定向到该文件。  
  
    **语法示例：**  
  
    `C:\>SSMAforAccessConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   如果没有 filepath xmloutput 切换后提供，则 xmlout 显示控制台本身上。  
  
    **语法示例：**  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>日志文件选项: – l/日志  
在控制台应用程序中的所有 SSMA 操作都记录在日志文件，并包含开关是可选。 如果在命令行指定了日志文件，它的路径，则在指定的位置获取生成日志。 否则，它获取生成在其默认位置。  
  
**语法示例：**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>项目环境文件夹选项: – e/projectenvironment  
此可选开关表示当前的 SSMA 项目的项目环境设置文件夹。  
  
**语法示例：**  
  
`C:\>SSMAforAccessConsole.EXE –s`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option-psecurepassword"></a>安全的密码选项: – p/securepassword  
此选项指示服务器连接的加密的密码。 它不同于所有其他选项，但它不会执行任何脚本或任何与迁移相关的活动，帮助可帮助管理的迁移项目中使用的服务器连接的密码加密。  
  
不能作为命令行参数输入任何其他选项或密码。 否则，它会导致错误。 有关详细信息，请参阅[管理密码](managing-passwords-accesstosql.md)部分。  
  
支持以下子选项`–p/securepassword`:  
  
-   若要添加密码，或更新现有密码，为受保护存储对于指定的服务器 ID，或者在服务器连接文件中定义的所有服务器 Id:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   从指定的服务器 ID 的所有服务器 Id; 二是受保护的存储中删除加密的密码：  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   要显示的密码加密的服务器 Id 列表：  
  
    `–p/securepassword –l/list`  
  
-   若要导出加密文件的受保护存储中存储的密码。 该文件是使用用户指定的密码加密。  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   加密文件之前导出导入到本地使用用户指定的密码的保护存储。 一旦该文件进行解密，它存储在一个新文件，又在本地计算机加密。  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    可以使用逗号分隔符指定多个服务器 Id。  
  
### <a name="help-option-help"></a>Help 选项:-？ / 帮助  
显示语法摘要 SSMA 控制台选项：  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
SSMA 控制台命令行选项以表格形式显示，请参阅[附录-1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)。  
  
### <a name="securepassword-help-option-securepassword--help"></a>SecurePassword Help 选项:-securepassword-？ / 帮助  
显示语法摘要 SSMA 控制台选项：  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
SSMA 控制台命令行选项以表格形式显示，请参阅[附录-1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>后续步骤  
下一步取决于你的项目要求：  
  
1.  用于指定密码或导出 / 导入密码，请参阅[管理密码&#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md)。  
  
2.  用于生成报告，请参阅[生成报表&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)。  
  
3.  有关故障排除控制台中的问题，请参阅[故障排除&#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md)。  
  
