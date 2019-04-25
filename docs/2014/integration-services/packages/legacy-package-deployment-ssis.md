---
title: 包部署 (SSIS) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c912d4417842bc332262549cc604b97eaa50a44d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767085"
---
# <a name="package-deployment-ssis"></a>包部署 (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括一些工具和向导，它们简化了将包从开发计算机部署到生产服务器或其他计算机的过程。  
  
 包部署过程中有四个步骤：  
  
1.  第一个可选步骤是可选的，包括创建在运行时更新包元素属性的包配置。 部署包时会自动包括这些配置。  
  
2.  第二步是生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，用于创建包部署实用工具。 项目的部署实用工具包含要部署的包  
  
3.  第三步是将生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目时创建的部署文件夹复制到目标计算机中。  
  
4.  第四步是在目标计算机上运行包安装向导，以将包安装到文件系统或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何创建部署实用工具的信息，请参阅 [创建部署实用工具](../create-a-deployment-utility.md)。  
  
 有关如何使用部署实用工具部署包的信息，请参阅 [使用部署实用工具部署包](../deploy-packages-by-using-the-deployment-utility.md)。  
  
 有关如何创建包配置的信息，请参阅 [创建包配置](../create-package-configurations.md)。  
  
  
