---
title: SSMA 控制台 (OracleToSQL) 中的命令行选项 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command Line Options, Help Option
- Command Line Options, SecurePassword Help Option
- Command Line Options, Variable Value File Option
- Command Line Options,Script File Option
ms.assetid: bf4a9313-349e-4ebf-9c89-9f5bb515f9ff
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 5606acac52bae2a97d0be1f6844970e81c051376
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982240"
---
# <a name="command-line-options-in-ssma-console-oracletosql"></a>SSMA 控制台 (OracleToSQL) 中的命令行选项
Microsoft 为您提供组强大的命令行选项来执行和控制 SSMA 活动。 接下来的几节详细介绍相同。  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA 控制台中的命令行选项  
此处所述的控制台命令选项。  
  
为便于本部分中，术语 '选项也称为转换。  
  
-   选项不区分大小写，并且可能开始是以**-** 或**/** 字符。  
  
-   如果指定了选项，则必须指定相应的选项参数。  
  
-   由空白，必须从选项字符分隔选项参数。  
  
    **语法示例：**  
  
    `C:\> SSMAforOracleConsole.EXE -s scriptfile`  
  
    `C:\> SSMAforOracleConsole.EXE -s “C Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \AssessmentReportGenerationSample.xml” –v “C Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \VariableValueFileSample.xml” –c “C Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ServersConnectionFileSample.xml”`  
  
-   包含空格的文件夹或文件名称应指定用双引号括起来。  
  
-   在标准输出中或指定文件中存储命令行条目和错误消息的输出。  
  
### <a name="script-file-option-sscript"></a>脚本文件选项:-s/脚本  
强制性开关，脚本文件路径/名称指定命令序列 SSMA 要执行该脚本。  
  
**语法示例：**  
  
`C:\>SSMAforOracleConsole.EXE –s “C Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>变量值文件选项:-v/变量  
此文件包含在脚本文件中使用的变量。 这是一个可选参数。 如果未在可变文件中声明变量和脚本文件中使用，应用程序将生成一个错误并终止控制台执行。  
  
**语法示例：**  
  
-   或许是默认值，另一个与实例特定值时适用的多个变量值文件中定义的变量。 命令行参数中指定的最后一个变量文件采用优先，以防重复的变量：  
  
    `C:\>SSMAforOracleConsole.EXE -s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>服务器连接文件选项:-c/serverconnection  
此文件包含服务器的每个服务器的连接信息。 每个服务器定义标识的唯一服务器 id。 在连接的脚本文件中引用服务器 Id 相关命令。  
  
服务器定义可以是服务器连接文件和/或脚本文件的一部分。 在脚本文件中的服务器 id 将优先于服务器连接文件，以防服务器 id 重复。  
  
**语法示例：**  
  
-   在脚本文件中使用服务器 Id 和单独的服务器连接文件中的定义、 服务器连接文件使用变量值文件中定义的变量：  
  
    `C:\>SSMAforOracleConsole.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   服务器定义嵌入的脚本文件：  
  
    `C:\>SSMAforOracleConsole.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 输出选项:-x / xmloutput [xmloutputfile]  
此命令用于将命令输出消息到控制台或 xml 文件以 xml 格式输出。  
  
有两个选项可用于 xmloutput，viz..,:  
  
-   如果文件路径提供 xmloutput 开关后输出重定向到文件。  
  
    **语法示例：**  
  
    `C:\>SSMAforOracleConsole.EXE –s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   如果没有文件路径提供 xmloutput 开关后本身在控制台上显示 xmlout。  
  
    **语法示例：**  
  
    `C:\>SSMAforOracleConsole.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>日志文件选项: – l/日志  
在控制台应用程序中的所有 SSMA 操作都记录在日志文件中。 这是一个可选参数。 如果在命令行指定了日志文件，它的路径，则在指定的位置获取生成日志。 否则，它获取生成在其默认位置。  
  
**语法示例：**  
  
`C:\>SSMAforOracleConsole.EXE`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>项目环境文件夹选项:-e/projectenvironment  
这表示当前 SSMA 项目项目的环境设置文件夹。 此开关是可选的。  
  
**语法示例：**  
  
`C:\>SSMAforOracleConsole.EXE –s`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option-psecurepassword"></a>安全的密码选项:-p/securepassword  
此选项指示服务器连接的加密的密码。 它不同于所有其它选项： 选项不执行任何脚本或有助于与迁移相关的所有活动中，但可帮助管理迁移项目中使用的服务器连接的密码加密。  
  
不能输入任何其他选项或密码作为命令行参数。 否则，它会导致错误。 有关详细信息，请参阅[管理密码](http://msdn.microsoft.com/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c)部分。  
  
支持下面的子选项`–p/securepassword`:  
  
-   若要添加密码保护存储为指定的服务器 ID 或服务器连接文件中定义的所有服务器 Id。 -如果已经存在，则覆盖选项，下面，更新密码：  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
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
  
### <a name="help-option-help"></a>帮助选项:-？ / 帮助  
显示语法摘要 SSMA 控制台选项：  
  
`C:\>SSMAforOracleConsole.EXE -?`  
  
SSMA 控制台命令行选项以表格形式显示，请参阅[附录-1 &#40;OracleToSQL&#41;](../../ssma/oracle/appendix-1-oracletosql.md)。  
  
### <a name="securepassword-help-option-securepassword--help"></a>SecurePassword Help 选项:-securepassword-？ / 帮助  
显示语法摘要 SSMA 控制台选项：  
  
`C:\>SSMAforOracleConsole.EXE -securepassword -?`  
  
SSMA 控制台命令行选项以表格形式显示，请参阅[附录-1 &#40;OracleToSQL&#41;](../../ssma/oracle/appendix-1-oracletosql.md)  
  
### <a name="next-step"></a>下一步  
下一步取决于你的项目要求：  
  
-   用于指定密码或导出 / 导入密码，请参阅[管理密码&#40;OracleToSQL&#41;](../../ssma/oracle/managing-passwords-oracletosql.md)。  
  
-   用于生成报告，请参阅[生成报表&#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md)。  
  
-   有关故障排除控制台中的问题，请参阅[故障排除&#40;OracleToSQL&#41;](../../ssma/oracle/troubleshooting-oracletosql.md)。  
  
