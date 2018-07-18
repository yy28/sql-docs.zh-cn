---
title: 将转换为包部署模型对话框 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1cb982b23645821f6c24c51b4ce4402336c08ea5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233857"
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
  
## <a name="see-also"></a>请参阅  
 [项目和包的部署](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [打包部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Integration Services 项目转换向导](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
