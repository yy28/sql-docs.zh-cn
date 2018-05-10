---
title: 报表生成器中的报表部件和数据集 | Microsoft Docs
ms.custom: ''
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2e5d0ee295fc34fbb0d319e9354cb2a5b6658e06
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="report-parts-and-datasets-in-report-builder"></a>报表生成器中的报表部件和数据集
  在报表生成器中，在报表中包含数据的最简单方式是从报表部件库添加报表部件。 报表部件包含它们所依赖的数据集，这些数据集称为 *相关数据集*。 相关数据集基于共享数据源，并且可以是嵌入数据集或共享数据集。 阅读有关 [报表部件](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)的详细信息。  
  
 在报表中包含数据的另一种简单的方式是使用一个共享数据集。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Adding"></a> 向报表中添加具有相关数据集的报表部件  
 在向您的报表中添加报表部件时，该部件所包含的相关数据集也添加到您的报表中。 因为报告部件可以包括含有许多其他报表项的矩形，所以，它可以将多个相关数据集添加到报表中。 每个共享数据集都是一个独立的引用；它依赖的共享数据源不会添加到报表中。 每个嵌入数据集也添加它所依赖的嵌入数据源或共享数据源。  
  
 嵌入数据源的凭据不作为报表部件的一部分保存。 如果某一嵌入数据源添加到您的报表中，则在运行该报表时系统将提示您输入凭据。 若要避免提示输入凭据，使用的报表部件应基于具有存储的凭据的共享数据源。  
  
 在向报表添加报表部件后，添加的数据集与您创建的嵌入数据集或共享数据集没有什么不同。 您可以在“报表数据”窗格中查看其他数据集。 嵌入数据集将出现在相应的共享数据源之下，共享数据集将出现在“共享数据集”文件夹之下。  
  
##  <a name="Customizing"></a> 自定义相关数据集  
 在向报表添加报表部件后，您可以预览它并决定是否对数据进行某些更改。 您能够进行的更改取决于您正在处理的数据集的类型。  
  
 若要更改某一嵌入数据集的数据和数据选项，您可以编辑包括查询在内的数据集属性，就像您自己创建了该数据集一样。  
  
 若要更改共享数据集的数据和数据选项，您只能在您具有足够权限的报表服务器上更改共享数据集定义。 您还可以通过添加筛选器、添加计算字段以及更改诸如区分大小写之类的数据选项，自定义您的报表中共享数据集的实例。 有关详细信息，请参阅[嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)。  
  
 有关如何更改共享数据集的定义或者如何在报表中显示共享数据集的最新数据更改的详细信息，请参阅[创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)和[在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
##  <a name="Publishing"></a> 将相关数据集作为共享数据集发布  
 当您发布具有相关数据集的报表项时，可以选择将每个数据集作为共享数据集发布，或者作为保持嵌入在报表项中的嵌入数据集发布。  
  
 在您选择共享数据集选项时，该数据集将作为共享数据集定义保存到报表服务器中。 在您的报表中，使用该数据集的每个报表项都更新为指向现在位于报表服务器上的共享数据集。 因此将发生以下两种情况：  
  
1.  在“发布”对话框中，已发布的每个共享数据集均从可供发布的项的列表中删除。  
  
2.  当您退出报表生成器或启动一个新报表时，系统将提示您保存您的报表。 如果您没有保存您的报表，则在下次打开此报表并发布报表项时，可能会发布相同数据集的新副本。 为了避免共享数据集的多个副本保存到报表服务器上，我们建议您保存该报表。  
  
> [!IMPORTANT]  
>  为了确保您和他人能够继续成功地使用来自共享数据集的数据，您必须理解确保报表项的安全所基于的原理。 有关详细信息，请参阅 [保护共享数据集项](../../reporting-services/security/secure-shared-dataset-items.md)。  
  
## <a name="see-also"></a>另请参阅  
 [报表设计视图（报表生成器）](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [安全性（报表生成器）](../../reporting-services/report-builder/security-report-builder.md)   
 [报表部件（报表生成器和 SSRS）](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
