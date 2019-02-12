---
title: 检查更新或关闭更新 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9c69792d-d7c4-453b-ae2f-6d2d071d8606
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 845013f002bc0d0937ae012ef033aaea1d45cc89
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025878"
---
# <a name="check-for-updates-or-turn-updates-off-report-builder-and-ssrs"></a>检查更新或关闭更新（报表生成器和 SSRS）
  每次您打开一个报表时，报表生成器都将查看该报表中报表部件的已发布实例是否已在报表服务器上或与报表服务器相集成的 SharePoint 站点上更新。 它还将检查报表部件的依赖项（如数据集和参数）的更改。 如果任何报表部件或其依赖关系已在站点或服务器上进行了更新，则报表中的信息栏将显示已更新部件的数量。 您可以选择查看并接受或拒绝更新，或关闭信息栏。  
  
 您还可以禁用信息栏，这样，当更改报表部件的已发布实例时系统将不会通知您。 这是一项用户设置；它将对您打开的所有报表禁用信息栏。 即使已禁用信息栏，也仍可以检查更新。  
  
### <a name="to-turn-on-and-off-report-part-updates"></a>打开和关闭报表部件更新  
  
1.  单击报表生成器按钮，然后单击**选项**。  
  
2.  在中**选项**对话框中，在**资源**选项卡上，选中或清除**我的报表中显示对报表部件的更新**复选框。  
  
> [!NOTE]  
>  这是一项用户设置。 它将对您打开的所有报表禁用信息栏。  
  
### <a name="to-check-for-updates"></a>若要检查更新  
  
-   右键单击设计图面上报表外或报表正文中，单击**检查是否有更新**。  
  
## <a name="see-also"></a>请参阅  
 [报表部件（报表生成器和 SSRS）](report-parts-report-builder-and-ssrs.md)   
 [发布和重新发布报表部件&#40;报表生成器和 SSRS&#41;](report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)   
 [浏览查找报表部件和设置默认文件夹&#40;报表生成器和 SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)   
 [报表部件故障排除&#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [报表生成器中的报表部件和数据集](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
