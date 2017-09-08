---
title: "SSMA 控制台 (AccessToSQL) 中的命令行选项 |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 827257d90042aa1655545edd9fc20d114952f426
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>SSMA 控制台 (AccessToSQL) 中的命令行选项
Microsoft 为你提供了一组可靠的命令行选项来执行和控制 SSMA 活动。 下来的几节提供了更多详细信息。  
  
## <a name="command-line-options-in-the-ssma-console"></a>SSMA 控制台中的命令行选项  
此处所述是控制台命令的选项。  
  
对于本部分，术语 option 也称为转换。  
  
选项不区分大小写，并且可能会启动与**-**'**/**字符。  
  
如果指定了选项，它是必填项指定相应的选项参数。  
  
选项参数必须用空格分隔从选项字符。  
  
**语法示例：**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
用双引号括起来，应指定文件夹或文件名称中包含空格。  
  
命令行条目和错误消息的输出会存储在 STDOUT 或在指定的文件。  
  
### <a name="script-file-option-sscript"></a>脚本文件选项:-s/脚本  
强制性开关，脚本文件路径/名称指定要由 SSMA 执行的命令序列的脚本。  
  
**语法示例：**  
  
`C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>变量值文件选项: – v/变量  
变量值文件包含在脚本文件中使用的变量。 交换机是可选的。 如果没有在变量文件中声明并在脚本文件中使用变量，该应用程序将生成错误并终止控制台执行。  
  
**语法示例：**  
  
-   在多个变量的值文件，可能是一个使用默认值，另一个具有特定于实例的值时适用中定义的变量。 中的命令行参数指定的最后一个变量文件采用首选项，以防还有变量的副本：  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>服务器连接文件选项: – c/serverconnection  
此文件包含每个服务器的服务器连接信息。 每个服务器定义标识由一个唯一的服务器 id。 服务器 Id 与连接相关的命令的脚本文件中引用。  
  
服务器定义可以是服务器连接文件和/或脚本文件的一部分。 脚本文件中的服务器 id 将优先于服务器连接文件，以防还有服务器 id 的副本。  
  
**语法示例：**  
  
-   脚本文件中使用服务器 Id。 它们在单独的服务器连接文件中定义。 此文件使用变量值文件中定义的变量：  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   在脚本文件中嵌入服务器定义：  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 输出选项:-x / xmloutput [xmloutputfile]  
此命令用于输出到控制台或 xml 文件以 xml 格式的命令输出消息。  
  
有两个选项可用于 xmloutput，即：  
  
-   如果 filepath xmloutput 切换后提供，输出是重定向到该文件。  
  
    **语法示例：**  
  
    `C:\>SSMAforAccessConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   如果没有 filepath xmloutput 切换后提供，则 xmlout 显示在控制台本身上。  
  
    **语法示例：**  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>日志文件选项: – l/日志  
在控制台应用程序的所有 SSMA 操作都记录在日志文件中，和开关，则可选。 如果在命令行指定了一个日志文件及安装路径，在指定的位置获取生成日志。 否则，它获取生成在其默认位置。  
  
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
  
### <a name="secure-password-option-psecurepassword"></a>安全密码选项: – p/securepassword  
此选项指示服务器连接的加密的密码。 它不同于所有其他选项，因为它不会执行任何脚本或帮助任何与迁移相关的活动，但可帮助管理在迁移项目中使用的服务器连接的密码加密。  
  
不能作为命令行参数中输入任何其他选项或密码。 否则，它会导致出现错误。 有关详细信息，请参阅[管理密码](http://msdn.microsoft.com/b099d0f9-dd37-4c87-8b6f-ed0177881ea4)部分。  
  
支持以下 suboptions `–p/securepassword`:  
  
-   若要添加密码，或更新现有密码，为受保护存储对于指定的服务器 ID，或者在服务器连接文件中定义的所有服务器 Id:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   从指定的服务器 ID 或服务器的所有 Id 的受保护的存储中删除加密的密码：  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   若要显示为其加密密码的服务器 Id 的列表：  
  
    `–p/securepassword –l/list`  
  
-   若要导出存储在受保护的存储加密文件的密码。 此文件是使用用户指定密码的短语加密。  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   加密文件前面导出导入到受保护的本地存储，使用用户指定密码。 一旦解密该文件，它会将其存储在新文件中，反过来，加密在本地计算机上。  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    可以使用逗号分隔符指定多个服务器 Id。  
  
### <a name="help-option-help"></a>Help 选项:-？ / 帮助  
显示 SSMA 控制台选项的语法的摘要：  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
有关的 SSMA 控制台命令行选项以表格形式显示，请参阅[附录-1 &#40;AccessToSQL &#41;](../../ssma/access/appendix-1-accesstosql.md).  
  
### <a name="securepassword-help-option-securepassword--help"></a>SecurePassword Help 选项:-securepassword-？ / 帮助  
显示 SSMA 控制台选项的语法的摘要：  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
有关的 SSMA 控制台命令行选项以表格形式显示，请参阅[附录-1 &#40;AccessToSQL &#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>后续步骤  
下一步取决于您的项目要求：  
  
1.  用于指定的密码或导出 / 导入密码，请参阅[管理密码 &#40;AccessToSQL &#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
2.  有关生成报表，请参阅[生成报表 &#40;AccessToSQL &#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
3.  有关故障排除控制台中的问题，请参阅[故障排除 &#40;AccessToSQL &#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  

