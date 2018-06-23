---
title: 启用 DirectQuery 设计模式 (SSAS 表格) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1ba954a8f296200070493625803aad263fa71520
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018289"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>启用 DirectQuery 设计模式（SSAS 表格）
  若要在 DirectQuery 模式下创建模型，您必须首先更改设计时环境，以便该环境支持 DirectQuery 模式的用户。 当您这样做时，该设计器还将执行以下操作：  
  
-   启用 DirectQuery 部署属性。  
  
-   更改工作区数据库，以便在使用缓存进行设计的混合模式下运行。 在您实际部署该模型时，该模式将更改回您在项目部署属性中指定的任何值。  
  
-   禁用与 DirectQuery 模式不兼容的设计功能。  
  
-   验证现有模型。  
  
 此过程描述如何在设计器中启用 DirectQuery 模式。  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>在模型中启用 DirectQuery  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，打开解决方案文件。  
  
2.  在对象资源管理器中，双击 Model.bim 文件。  
  
3.  在 **“属性”** 窗格中，将属性 **DirectQueryMode**更改为 **On**。  
  
4.  如果没有错误，Visual Studio 中，打开**错误列表**并解决将阻止模型切换到 DirectQuery 模式的任何问题。  
  
## <a name="see-also"></a>请参阅  
 [DirectQuery 模式下&#40;SSAS 表格&#41;](directquery-mode-ssas-tabular.md)  
  
  