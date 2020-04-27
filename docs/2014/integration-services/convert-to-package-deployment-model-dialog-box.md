---
title: "\"转换为包部署模型\" 对话框 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dfe1f6e5b752284b6bb0feec96f4f3dfd67cc4f6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060352"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>“转换为包部署模型”对话框
  使用 **“转换为包部署模型”** 命令可以在检查项目和项目中的每个包与包部署模型是否兼容后将包转换为该模型。 如果包使用项目部署模型特有的功能（如参数），则不能转换该包。  
  
## <a name="task-list"></a>任务列表  
 将包转换为包部署模型需要两个步骤。  
  
1.  从 **“项目”** 菜单选择 **“转换为包部署模型”** 命令时，检查项目和其中的每个包是否与此模型兼容。 结果显示在 **“结果”** 表中。  
  
     如果项目或其中的某个包未通过兼容测试，单击 **“结果”** 列中的 **“失败”** 可以获取详细信息。 单击 **“保存报告”** ，以将此信息的副本保存到文本文件。  
  
2.  如果项目和所有包都通过了兼容测试，则单击 **“确定”** 以转换包。  
  
> [!NOTE]  
>  若要将项目转换为项目部署模型，请使用 **“Integration Services 项目转换向导”**。 有关详细信息，请参阅 [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md)。  
  
## <a name="see-also"></a>另请参阅  
 [项目和包的部署](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [包部署 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Integration Services 项目转换向导](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
