---
title: 复制项目项 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Integration Services], copying
- packages [Integration Services], copying
- copying data source views
- copying data sources
- copying packages
- data source views [Integration Services], copying
ms.assetid: 1606c54d-20f9-49f3-a4ef-caad83a772aa
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3456209c467c3b8474e130181d02304911098d2c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437974"
---
# <a name="copy-project-items"></a>复制项目项
  本主题说明如何在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目内或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目之间复制对象。 您还可以在其他类型的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 项目（ [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]）之间复制对象。 若要在项目之间进行复制，则项目必须是同一个 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 解决方案的一部分。 有关详细信息，请参阅 [Integration Services (SSIS) 项目](integration-services-ssis-projects-and-solutions.md)。  
  
### <a name="to-copy-project-level-items"></a>复制项目级别的项  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开希望处理的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目或解决方案。  
  
2.  展开要从中复制对象的项目和项文件夹。  
  
3.  右键单击该项，然后单击“复制”****。  
  
4.  右键单击要复制到其中的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，然后单击“粘贴”****。  
  
     这些项会自动复制到正确的文件夹中。 如果将项复制到不是包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中，则该项将复制到 **“杂项”** 文件夹中。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS&#41; 包](../../2014/integration-services/integration-services-ssis-packages.md)   
 [复制包对象](../../2014/integration-services/copy-package-objects.md)  
  
  
