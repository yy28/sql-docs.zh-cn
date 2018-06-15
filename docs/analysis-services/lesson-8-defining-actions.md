---
title: 第 8 课： 定义操作 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 50cc788fa39531c086049886a77f17920ae81e8f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34017494"
---
# <a name="lesson-8-defining-actions"></a>第 8 课：定义操作
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在本课中，将了解如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目中定义操作。 操作只是存储在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中并且可以合并到客户端应用程序中并被用户启动的多维表达式 (MDX) 语句。  
  
> [!NOTE]  
> 本教程的所有课程中的已完成项目均可以从网上获得。 您可以通过将前一课程的已完成项目作为起始点，跳转到后面的任何课程。 [单击此处](http://go.microsoft.com/fwlink/?LinkID=221866) 可以下载本教程随附的示例项目。  
  
[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持下表描述的操作类型。  
  
|||  
|-|-|  
|CommandLine|在命令提示符下执行命令|  
|数据集|将数据集返回到客户端应用程序。|  
|钻取|将钻取语句作为表达式返回，客户端将执行此语句以返回行集|  
|Html|在 Internet 浏览器中执行 HTML 脚本|  
|专有|使用除此表列出的这些类型以外的其他接口执行操作。|  
|报告|将基于参数化 URL 的请求提交到报表服务器，并将报表返回到客户端应用程序。|  
|行集|将行集返回到客户端应用程序。|  
|。|运行 OLE DB 命令。|  
|URL|在 Internet 浏览器中显示动态网页。|  
  
操作让用户能够在所选项的上下文中启动应用程序或执行其他步骤。 有关详细信息，请参阅[操作（Analysis Services — 多维数据）](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)和[多维模型中的操作](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
> [!NOTE]  
> 有关操作的示例，请参阅“计算工具”窗格中的“模板”选项卡上的操作示例或 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 示例数据仓库中的示例。 有关如何安装此数据库的详细信息，请参阅 [安装 Analysis Services 多维建模教程的示例数据和项目](../analysis-services/install-sample-data-and-projects.md)。  
  
本课包括以下任务：  
  
[定义和使用钻取操作](../analysis-services/lesson-8-1-defining-and-using-a-drillthrough-action.md)  
在此任务中，将通过先前在此教程中定义的事实维度关系，来定义、使用然后修改钻取操作。  
  
## <a name="next-lesson"></a>下一课  
[Lesson 9: Defining Perspectives and Translations](../analysis-services/lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>另请参阅  
[Analysis Services 教程方案](../analysis-services/analysis-services-tutorial-scenario.md)  
[多维建模（Adventure Works 教程）](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
[操作 & #40;Analysis Services-多维数据 & #41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[多维模型中的操作](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
  
  
