---
title: 检查更新或关闭 （报表生成器和 SSRS） 的轮次更新 |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c69792d-d7c4-453b-ae2f-6d2d071d8606
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: c355099f67128f90a958d59f91de5f0d21c68a19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124735"
---
# <a name="check-for-updates-or-turn-updates-off-report-builder-and-ssrs"></a>检查更新或关闭更新（报表生成器和 SSRS）
  每次您打开一个报表时，报表生成器都将查看该报表中报表部件的已发布实例是否已在报表服务器上或与报表服务器相集成的 SharePoint 站点上更新。 它还将检查报表部件的依赖项（如数据集和参数）的更改。 如果任何报表部件或其依赖关系已在站点或服务器上进行了更新，则报表中的信息栏将显示已更新部件的数量。 您可以选择查看并接受或拒绝更新，或关闭信息栏。  
  
 您还可以禁用信息栏，这样，当更改报表部件的已发布实例时系统将不会通知您。 这是一项用户设置；它将对您打开的所有报表禁用信息栏。 即使已禁用信息栏，也仍可以检查更新。  
  
### <a name="to-turn-on-and-off-report-part-updates"></a>打开和关闭报表部件更新  
  
1.  单击报表生成器按钮，然后单击**选项**。  
  
2.  在**选项**对话框中，在**资源**选项卡上，选中或清除**我的报表中显示为报表部件的更新**复选框。  
  
> [!NOTE]  
>  这是一项用户设置。 它将对您打开的所有报表禁用信息栏。  
  
### <a name="to-check-for-updates"></a>若要检查更新  
  
-   右键单击设计图面外报表，或在报表正文中，然后单击**检查更新**。  
  
## <a name="see-also"></a>请参阅  
 [报表部件&#40;报表生成器和 SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [发布和重新发布报表部件&#40;报表生成器和 SSRS&#41;](report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)   
 [查找报表部件和设置默认文件夹&#40;报表生成器和 SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)   
 [解决报表部件&#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [报表生成器中的报表部件和数据集](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  