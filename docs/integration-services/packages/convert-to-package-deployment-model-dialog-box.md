---
title: "“转换为包部署模型”对话框 | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.bids.converttolegacydeployment.f1"
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# “转换为包部署模型”对话框
  使用 **“转换为包部署模型”** 命令可以在检查项目和项目中的每个包与包部署模型是否兼容后将包转换为该模型。 如果包使用项目部署模型特有的功能（如参数），则不能转换该包。  
  
## 任务列表  
 将包转换为包部署模型需要两个步骤。  
  
1.  从 **“项目”** 菜单选择 **“转换为包部署模型”** 命令时，检查项目和其中的每个包是否与此模型兼容。 结果显示在 **“结果”** 表中。  
  
     如果项目或其中的某个包未通过兼容测试，单击 **“结果”** 列中的 **“失败”** 可以获取详细信息。 单击 **“保存报告”** ，以将此信息的副本保存到文本文件。  
  
2.  如果项目和所有包都通过了兼容测试，则单击 **“确定”** 以转换包。  
  
> **注意：**若要将项目转换为项目部署模型，请使用 **Integration Services 项目转换向导**。 有关详细信息，请参阅 [Integration Services Project Conversion Wizard](https://msdn.microsoft.com/library/hh213290.aspx)。  
  
## 另请参阅  
 [早期包部署 (SSIS)](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Integration Services 项目转换向导](../../integration-services/packages/integration-services-project-conversion-wizard.md)  
  
  