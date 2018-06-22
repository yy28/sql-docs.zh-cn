---
title: 重新部署包 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f8b5ffb9f238fdc87ecb51765733f3a9cb632946
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014087"
---
# <a name="redeployment-of-packages"></a>重新部署包
  在部署项目后，您可能需要更新或扩展包功能，然后重新部署包含更新包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。 在重新部署包的过程中，您应该检查部署实用工具中包括的配置属性。 例如，您可能不希望在重新部署包后允许对配置进行更改。  
  
## <a name="process-for-redeployment"></a>重新部署过程  
 在完成更新包后，您应该重新生成该项目，将部署文件夹复制到目标计算机，然后重新运行包安装向导。  
  
 如果只更新项目中的少数几个包，您可能不希望重新部署整个项目。 若要仅部署几个包，可以新建一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，将更新后的包添加到新的项目，然后生成并部署该项目。 在将包添加到其他项目时，包配置会自动随包一起复制。  
  
## <a name="related-tasks"></a>Related Tasks  
 [使用部署实用工具部署包](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  