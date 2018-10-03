---
title: 创建脚本文件 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Script File Creation, Configuring Oracle Console Settings
- Script File Creation, Non-Configurable option
- Script File Creation, Script File Validation
ms.assetid: 55e5bc68-3040-4f07-bb00-0408a17c9821
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 879aaaf33365cb7453c1047c3f9b2408edee10f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846767"
---
# <a name="creating-script-files-oracletosql"></a>创建脚本文件 (OracleToSQL)
第一步是启动 SSMA 控制台应用程序创建脚本文件之前，如果需要创建变量值文件和服务器连接文件。  
  
脚本文件可分为三个部分，报道..,:  
  
1.  **配置：** 使用户能够设置控制台应用程序的配置参数。  
  
2.  **服务器：** 使用户能够设置源/目标服务器定义。 这也可以是单独的服务器连接文件中。  
  
3.  **脚本命令：** 使用户能够执行 SSMA 工作流命令。  
  
下面将详细介绍每个部分：  
  
## <a name="configuring-oracle-console-settings"></a>配置 Oracle 控制台设置  
脚本的配置将显示在控制台脚本文件。  
  
如果配置节点中指定的任何元素，它们设置与全局设置即它们是适用于所有的脚本命令。 这些配置元素也可以设置每个命令中的脚本命令部分中如果用户想要重写全局设置。  
  
用户可配置选项包括：  
  
1.  **输出窗口提供程序：** 如果禁止显示消息属性设置为 'true'，特定于命令的执行不在控制台上显示消息。 下面给出了属性说明：  
  
    -   目标： 指定输出是否需要获取打印到文件或 stdout。 这是默认值为 false。  
  
    -   文件名称: （可选） 的文件的路径。  
  
    -   禁止显示消息： 禁止显示在控制台上的消息。 这是 'false'，默认情况下。  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **数据迁移连接提供程序：** 这指定哪些源/目标服务器将被视为数据迁移。  源-使用-上次使用指示的最后一个使用的源服务器用于数据迁移。 同样目标-使用-上次使用指示的最后一个使用的目标服务器用于数据迁移。 用户还可以通过使用属性源服务器或目标服务器指定的服务器 （源或目标）。  
  
    即使用只有一个或另一个指定的属性：  
  
    -   源-使用-上次使用 ="true"（默认值） 或源服务器 ="source_servername"  
  
    -   目标-使用-上次使用 ="true"（默认值） 或目标服务器 ="target_servername"  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection source-use-last-used="true"  
  
                                 target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **用户输入弹出窗口：** 这样的错误，处理时从数据库加载对象。 用户提供的输入的模式，并发生错误，在控制台继续按用户指定。  
  
    模式包括：  
  
    -   **要求-用户-** continue('yes') 或出错 （否） 对用户进行提示。  
  
    -   **错误-** 控制台显示错误并停止执行。  
  
    -   **继续-** 控制台将继续执行。  
  
    默认模式是**错误**。  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **重新连接提供程序：** 这允许用户设置的重新连接设置由于连接失败。 这可以为源和目标服务器设置。  
  
    重新连接模式如下：  
  
    -   重新连接到上一次-使用的服务器： 如果连接未处于活动状态，它将尝试重新连接到最后一个服务器使用最多 5 次。  
  
    -   生成一个错误： 如果连接未处于活动状态，会生成错误。  
  
    默认模式是**生成一个错误**。  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                         on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *or*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **转换器覆盖提供程序：** 这使用户能够处理对象已在目标上存在的元数据库。 可能的操作包括：  
  
    -   错误： 在控制台显示错误并停止执行。  
  
    -   覆盖： 将覆盖现有对象值。 默认情况下完成此操作。  
  
    -   跳过： 在控制台上，对数据库将跳过已存在的对象  
  
    -   询问用户： 提示用户输入 (是 / 否)  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **失败的系统必备组件提供程序：** 这使用户能够处理任何处理命令所需的先决条件。 默认情况下，严格模式下为 false。 如果将其设置为 true，异常生成失败，若要满足的先决条件。  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **停止操作：** 中间在操作期间，如果用户想要停止此操作，然后**Ctrl + C**可以使用热键。 SSMA for Oracle 控制台将等待操作完成，并终止控制台执行。  
  
    如果用户想要执行立即停止，然后**Ctrl + C**热键可以再次按下的 SSMA 控制台应用程序突然终止。  
  
8.  **正在进行的提供程序：** 通知每个控制台命令的进度。 默认情况下禁用该功能。 包含进度报告属性：  
  
    -   off  
  
    -   每个 1%  
  
    -   每个 2%  
  
    -   每个 5%  
  
    -   每个 10%  
  
    -   每个 20%  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"            (optional)  
  
                          report-messages="<true/false>"   (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <…All commands…>  
  
      <progress-reporting  
  
        enable="<true/false>"            (optional)  
  
        report-messages="<true/false>"   (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off"     (optional)/>  
  
    </…All commands…>  
    ```  
  
9. **记录器详细级别：** 设定日志详细级别。 这相当于在 UI 中的所有类别选项。 默认情况下，日志详细级别为"错误"。  
  
    记录器级选项包括：  
  
    -   致命错误： 仅致命错误消息记录。  
  
    -   错误： 唯一的错误和严重错误消息记录。  
  
    -   警告： 将记录所有级别调试和信息消息除外。  
  
    -   信息： 只记录调试消息的所有级别。  
  
    -   调试： 记录的消息的所有级别。  
  
    > [!NOTE]  
    > 在任何级别上记录必需的消息。  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **重写加密密码：** 明文密码 'true'，如果指定的节服务器定义的服务器连接文件或脚本文件中重写的加密的密码存储在受保护存储，如果存在。 如果没有密码以明文形式指定，将提示用户输入密码。  
  
    下面两种情况下出现：  
  
    1.  如果重写选项是**false**，搜索的顺序就会是受保护存储&gt;脚本文件-&gt;服务器连接文件-&gt;提示用户。  
  
    2.  如果重写选项是 **，则返回 true**，搜索的顺序将为脚本文件-&gt;服务器连接文件-&gt;提示用户。  
  
    **示例：**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
非可配置选项是：  
  
-   **最大重新连接尝试次数：** 时建立的连接超时，或由于网络故障将中断，则需要重新连接服务器。 重新连接尝试的最多允许**5**重试次数后，控制台将自动执行重新连接。 自动重新连接的工具减少了在工作中重新运行该脚本。  
  
## <a name="server-connection-parameters"></a>服务器连接参数  
在脚本文件或服务器连接文件中，可以定义服务器连接参数。 请参阅[创建服务器连接文件&#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)部分，了解更多详细信息。  
  
## <a name="script-commands"></a>脚本命令  
脚本文件包含一系列以 XML 格式的迁移工作流命令。 SSMA 控制台应用程序处理以使其不显示在脚本文件中的命令顺序迁移。  
  
例如，Oracle 数据库中的特定表的典型的数据迁移如下所示的层次结构： 架构-&gt;表。  
  
当成功执行脚本文件中的所有命令时，SSMA 控制台应用程序退出，并将该控件返回给用户。 脚本文件的内容可能会更多或更少静态变量的信息包含在[创建变量值文件&#40;OracleToSQL&#41; ](../../ssma/oracle/creating-variable-value-files-oracletosql.md)或变量值的脚本文件中的单独部分中。  
  
**示例：**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
产品目录的示例控制台脚本文件夹中提供模板变量值文件和服务器连接文件 （用于执行各种方案） 的 3 个脚本文件组成：  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
更改显示其中的关联性的参数后，可以执行模板 （文件）。  
  
脚本命令的完整列表可在[执行 SSMA 控制台&#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="script-file-validation"></a>脚本文件验证  
用户可以轻松地验证他/她脚本文件是否符合架构定义文件**O2SSConsoleScriptSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
在操作控制台中的下一步是[创建的变量值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[创建变量值文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
