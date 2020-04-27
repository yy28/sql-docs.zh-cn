---
title: Analysis Services 执行 DDL 任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a74ab896e974410e8357a22546cb63ed7365a149
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833152"
---
# <a name="analysis-services-execute-ddl-task"></a>Analysis Services 执行 DDL 任务
  “ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务运行数据定义语言 (DDL) 语句，这些语句可以创建、删除或更改挖掘模型和多维对象，如多维数据集和维度。 例如，DDL 语句可在 **Adventure Works** 多维数据集中创建分区，或删除 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]（即 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中包含的示例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库）中的维度。  
  
 “ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 有关详细信息，请参阅 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含许多执行商业智能操作（如处理分析对象和运行数据挖掘预测查询）的任务。  
  
 有关相关商业智能任务的详细信息，请单击以下主题之一：  
  
-   [Analysis Services 处理任务](analysis-services-processing-task.md)  
  
-   [数据挖掘查询任务](data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>DDL 语句  
 DDL 语句表示为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 中的语句，并且嵌入 XML for Analysis (XMLA) 命令中。  
  
-   ASSL 用于定义和说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例及其包含的数据库和数据库对象。 有关详细信息，请参阅[Analysis Services 脚本语言 &#40;ASSL&#41; 引用](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)。  
  
-   XMLA 是用于向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例发送操作命令（如 Create、Alter 或 Process）的命令语言。 有关详细信息，请参阅 [XML for Analysis (XMLA) 参考](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)。  
  
 如果 DDL 代码存储在单独的文件中，则“ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务使用文件连接管理器来指定该文件的路径。 有关详细信息，请参阅 [File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 因为 DDL 语句可以包含密码和其他敏感信息，所以包含一个或多个“[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行 DDL”任务的包应该使用包保护级别 `EncryptAllWithUserKey` 或 `EncryptAllWithPassword`。 有关详细信息，请参阅 [Integration Services (SSIS) 包](../integration-services-ssis-packages.md)。  
  
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
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [Analysis Services 执行 DDL 任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [Analysis Services 执行 DDL 任务编辑器（DDL 页）](../analysis-services-execute-ddl-task-editor-ddl-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击以下主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>“Analysis Services 执行 DDL”任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
  
