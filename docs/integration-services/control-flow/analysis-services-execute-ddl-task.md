---
title: Analysis Services 执行 DDL 任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asexecuteddltask.f1
- sql13.dts.designer.asexecuteddltask.general.f1
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a160e61e390f58dc640a5d1da265cdb77d5d9be1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294344"
---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services 执行 DDL 任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  “ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务运行数据定义语言 (DDL) 语句，这些语句可以创建、删除或更改挖掘模型和多维对象，如多维数据集和维度。 例如，DDL 语句可在 **Adventure Works** 多维数据集中创建分区，或删除 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]（即 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中包含的示例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库）中的维度。  
  
 “ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 有关详细信息，请参阅 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含许多执行商业智能操作（如处理分析对象和运行数据挖掘预测查询）的任务。  
  
 有关相关商业智能任务的详细信息，请单击以下主题之一：  
  
-   [Analysis Services 处理任务](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [数据挖掘查询任务](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL 语句  
 DDL 语句表示为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 中的语句，并且嵌入 XML for Analysis (XMLA) 命令中。  
  
-   ASSL 用于定义和说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例及其包含的数据库和数据库对象。 有关详细信息，请参阅 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)。  
  
-   XMLA 是用于向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例发送操作命令（如 Create、Alter 或 Process）的命令语言。 有关详细信息，请参阅 [XML for Analysis (XMLA) 参考](/bi-reference/xmla/xml-for-analysis-xmla-reference)。  
  
 如果 DDL 代码存储在单独的文件中，则“ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务使用文件连接管理器来指定该文件的路径。 有关详细信息，请参阅 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
 因为 DDL 语句可以包含密码和其他敏感信息，所以包含一个或多个“[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务的包应该使用包保护级别 **EncryptAllWithUserKey** 或 **EncryptAllWithPassword**。 有关详细信息，请参阅 [Integration Services (SSIS) 包](../../integration-services/integration-services-ssis-packages.md)。  
  
### <a name="ddl-examples"></a>DDL 示例  
 以下三个 DDL 语句是通过对 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]（包含在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库）中的对象编写脚本而生成。  
  
 下面的 DDL 语句删除 **Promotion** 维度。  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 以下 DDL 语句处理 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 多维数据集。  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 下面的 DDL 语句创建 **Forecasting** 挖掘模型。  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
 以下三个 DDL 语句是通过对 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]（包含在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库）中的对象编写脚本而生成。  
  
 下面的 DDL 语句删除 **Promotion** 维度。  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 以下 DDL 语句处理 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 多维数据集。  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 下面的 DDL 语句创建 **Forecasting** 挖掘模型。  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
## <a name="configuration-of-the-analysis-services-execute-ddl-task"></a>“Analysis Services 执行 DDL”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击以下主题：  
  
-   [设置任务或容器的属性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>“Analysis Services 执行 DDL”任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
## <a name="analysis-services-execute-ddl-task-editor-general-page"></a>Analysis Services 执行 DDL 任务编辑器（“常规”页）
  可以使用“Analysis Services 执行 DDL 任务编辑器”  对话框的“常规”  页命名和描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL 任务。  
  
### <a name="options"></a>选项  
 **名称**  
 为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL 任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL 任务的说明。  
  
## <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services 执行 DDL 任务编辑器（DDL 页）
  可以使用“Analysis Services 执行 DDL 任务编辑器”对话框的 **DDL** 页指定与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的连接，以及提供有关数据定义语言 (DDL) 语句的源的信息。   
  
### <a name="static-options"></a>静态选项  
 **“连接”**  
 在列表中选择 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器，或单击“\<新建连接...>”  并使用“添加 Analysis Services 连接管理器”  对话框新建一个连接。  
  
 **相关主题：** [“添加 Analysis Services 连接管理器”对话框 UI 参考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)、[Analysis Services 连接管理器](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 指定 DDL 语句的源类型。 此属性具有下表所列的选项：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接输入**|将源设置为 **SourceDirect** 文本框中存储的 DDL 语句。 选择此值将显示以下部分中的动态选项。|  
|**文件连接**|将源设置为包含 DDL 语句的文件。 选择此值将显示以下部分中的动态选项。|  
|**变量**|将源设置为变量。 选择此值将显示以下部分中的动态选项。|  
  
### <a name="dynamic-options"></a>动态选项  
  
#### <a name="sourcetype--direct-input"></a>SourceType = 直接输入  
 **数据源**  
 键入 DDL 语句，或单击省略号 (…)，然后在“DDL 语句”对话框中键入语句   。  
  
#### <a name="sourcetype--file-connection"></a>SourceType = 文件连接  
 **数据源**  
 在列表中选择“文件连接”，或单击“\<新建连接...>”  并使用“文件连接管理器”  对话框新建一个连接。  
  
 **相关主题：** [文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)  
  
#### <a name="sourcetype--variable"></a>SourceType = 变量  
 **数据源**  
 在列表中选择一个变量，或单击“\<新建变量...>”并使用“添加变量”对话框新建一个变量   。  
  
 **相关主题：** [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)  
  
