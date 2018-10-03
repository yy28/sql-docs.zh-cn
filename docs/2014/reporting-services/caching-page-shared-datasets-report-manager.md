---
title: 缓存页，共享数据集 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8d19f339b8cb8955ab33f73ea164f8bbfb2e7fce
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205168"
---
# <a name="caching-page-shared-datasets-report-manager"></a>共享数据集的“缓存”页（报表管理器）
  使用“缓存”属性页可以设置共享数据集的缓存选项。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面中的这一位置。  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>打开共享数据集的“缓存”属性页  
  
1.  打开报表管理器，找到您要配置共享数据集属性的报表。  
  
2.  指向该共享数据集，然后单击下拉箭头。  
  
3.  在下拉列表中，单击 **“管理”**。 这会打开该报表的“常规”属性页。  
  
4.  单击 **“缓存”** 选项卡。  
  
## <a name="options"></a>选项  
 **缓存共享数据集**  
 用户首次打开使用此共享数据集的报表时，在缓存中放置数据的临时副本。 以后在缓存期内运行报表的用户将收到数据的缓存副本。 由于将从缓存中返回数据（而不是重新运行数据集查询），因此进行缓存通常会提高性能。  
  
 **缓存到期后的分钟数**  
 指定要保存数据缓存副本的分钟数。 临时副本一到期，就不会再从缓存中返回数据。 下次用户打开使用此共享数据集的报表时，将运行数据集查询，之后报表服务器将刷新后的数据副本存入缓存。  
  
 **缓存根据以下计划到期**  
 预设缓存的数据不再有效并且从缓存中删除的时间。 计划可以是共享计划，也可以是仅适用于当前共享数据集的特定计划。  
  
 **数据集特定计划**  
 指定仅用于此数据集的计划。  
  
 **共享的计划**  
 指定在报表、订阅和其他共享数据集之间共享的计划。  
  
 **应用**  
 保存更改。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [缓存共享数据集 (SSRS)](report-server/cache-shared-datasets-ssrs.md)   
 [计划](subscriptions/schedules.md)  
  
  
