---
title: 常规属性页上，共享数据集 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 10798e41-24c3-4e69-893b-7ee6af7fc958
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7ed5b54ea07249a69e6f599e53658e8aba10d656
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63260761"
---
# <a name="general-properties-page-shared-datasets-report-manager"></a>共享数据集的“常规”属性页（报表管理器）
  使用“共享数据集”页可以查看和管理共享数据集项的属性。  
  
 从报表管理器不能查看或更改共享数据集定义（包括查询）。 若要更改定义，必须使用创作工具打开和修改定义，然后将定义保存到报表服务器。  
  
 使用共享数据集，您可以单独管理数据集的设置，使其和报表、组件以及使用它的其他目录项分开。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-shared-dataset-properties-page-for-a-shared-dataset"></a>打开共享数据集的“共享数据集”属性页  
  
1.  打开报表管理器，找到您要配置属性的共享数据集。  
  
2.  悬停在该共享数据集之上，然后单击下拉箭头。  
  
3.  在下拉列表中，单击 **“管理”**。 此时，将打开“常规”属性页。  
  
## <a name="options"></a>选项  
 **名称**  
 键入共享数据集的名称，此名称用于标识报表服务器文件夹层次结构内的项。  
  
 **说明**  
 提供有关共享数据集的信息。 此说明显示在“内容”页上。  
  
 **在列表视图中隐藏**  
 对正在报表管理器中使用列表视图模式的用户隐藏共享数据集。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 在列表视图中，项的名称和说明可跨越页面。 备用格式为详细信息视图。 详细信息视图省略了说明，但包含项的其他信息。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制访问项，必须创建角色分配。  
  
 **查询执行超时值**  
 键入查询在多长时间后超时（秒）。如果该值为 0，则查询将不会超时。  
  
 **Apply**  
 保存更改。  
  
 **删除**  
 从报表服务器数据库中删除共享数据集。 删除共享数据集将停用所有报表或缓存的版本。 若要重新激活报表，必须在报表创作工具中打开每个报表，用相同的名称和相同的字段集合指定数据集。 或者，可以更新每个数据区域引用以使用另一个具有相同字段集合的数据集。  
  
 **“移动”**  
 在报表服务器文件夹层次结构中重新定位共享数据集。 单击此按钮将打开“移动项”页，可以在该页浏览文件夹以选择新的文件夹位置。 有关详细信息，请参阅[移动项页&#40;报表管理器&#41;](../../2014/reporting-services/move-items-page-report-manager.md)。  
  
 **下载**  
 提取共享数据集定义的副本。 根据计算机上所定义的文件关联的不同，文件将在 Visual Studio 或其他应用程序中打开。 大多数情况下，共享数据集将以 XML 文件形式打开。  
  
 **替换**  
 将共享数据集定义替换为文件系统上 .rsd 文件中的其他定义。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [“内容”页（报表管理器）](../../2014/reporting-services/contents-page-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [缓存刷新选项&#40;报表管理器&#41;](../../2014/reporting-services/cache-refresh-options-report-manager.md)   
 [缓存页，共享数据集&#40;报表管理器&#41;](../../2014/reporting-services/caching-page-shared-datasets-report-manager.md)   
 [管理共享数据集](report-data/manage-shared-datasets.md)   
 [缓存共享数据集 (SSRS)](report-server/cache-shared-datasets-ssrs.md)  
  
  
