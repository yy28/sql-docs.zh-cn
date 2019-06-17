---
title: 第 8 课：定义操作 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8293bb8d1f0465d09b296cbd18702b569f073766
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078231"
---
# <a name="lesson-8-defining-actions"></a>第 8 课：定义操作
  在本课中，将了解如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目中定义操作。 操作只是存储在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中并且可以合并到客户端应用程序中并被用户启动的多维表达式 (MDX) 语句。  
  
> [!NOTE]  
>  本教程的所有课程中的已完成项目均可以从网上获得。 您可以通过将前一课程的已完成项目作为起始点，跳转到后面的任何课程。 [单击此处](https://go.microsoft.com/fwlink/?LinkID=221866) 可以下载本教程随附的示例项目。  
  
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
|声明专用纸|运行 OLE DB 命令。|  
|URL|在 Internet 浏览器中显示动态网页。|  
  
 操作让用户能够在所选项的上下文中启动应用程序或执行其他步骤。 有关详细信息，请参阅[操作（Analysis Services — 多维数据）](multidimensional-models/actions-analysis-services-multidimensional-data.md)和[多维模型中的操作](multidimensional-models/actions-in-multidimensional-models.md)  
  
> [!NOTE]  
>  有关操作的示例，请参阅“计算工具”窗格中的“模板”选项卡上的操作示例或 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 示例数据仓库中的示例。 有关如何安装此数据库的详细信息，请参阅 [安装 Analysis Services 多维建模教程的示例数据和项目](install-sample-data-and-projects.md)。  
  
 本课包括以下任务：  
  
 [定义和使用钻取操作](lesson-8-1-defining-and-using-a-drillthrough-action.md)  
 在此任务中，将通过先前在此教程中定义的事实维度关系，来定义、使用然后修改钻取操作。  
  
## <a name="next-lesson"></a>下一课  
 [第 9 课：定义透视和翻译](lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 教程方案](analysis-services-tutorial-scenario.md)   
 [多维建模&#40;Adventure Works 教程&#41;](multidimensional-modeling-adventure-works-tutorial.md)   
 [操作&#40;Analysis Services-多维数据&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)   
 [多维模型中的操作](multidimensional-models/actions-in-multidimensional-models.md)  
  
  
