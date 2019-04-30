---
title: 点击链接型报表页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7f76a4c0d2e9cc3bd2d5591a704491a4bed0ebfb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63266142"
---
# <a name="clickthrough-reports-page-report-manager"></a>“点击链接型报表”页（报表管理器）
  当您单击报表中所包含的交互式数据时，点击链接型报表显示相关的数据表。 这些报表由报表服务器基于用来创建报表的模型中所包含的信息来生成。 如果您不想使用由报表服务器生成的点击链接型报表，则可以创建自定义报表，将其发布到报表服务器并映射到在模型中定义的交互式数据点。 必须在报表生成器中从同一模型创建自定义报表，然后再发布到报表服务器。 若要将自定义报表映射到模型中的项，请使用报表管理器中的“点击链接型报表”页。  
  
 “点击链接型报表”页提供一种将预定义的已发布报表生成器报表映射到模型中特定实体、文件夹和项的方法。 将报表映射到模型中的项时，导航到该项的用户将获得自定义报表，而不是由报表服务器生成的临时报表。  
  
 若要提供自定义报表，则应包括该报表的单个实例版本和多个实例版本。 用户导航到特定实体所用的数据路径将确定在运行时提供给用户的是单个实例报表还是多个实例报表。 您事先并不一定知道是否不需要特定版本的报表。  
  
 映射到实体的自定义报表可以通过报表服务器文件夹层次结构进行保护。 如果将模型项映射到某个报表，并且该报表对于已导航到它的用户不可用，则该用户将得到由报表服务器生成的临时报表，而不是预期的自定义报表。  
  
 尽管您可以选择任何可访问的报表，但请仅选择专门为您正在配置的模型创建的报表。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均不提供点击链接型报表。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 如果不能确定您的单位所运行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的版本，请与数据库管理员联系。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>打开“点击链接型报表”页  
  
1.  打开报表管理器，找到您要将点击链接型报表映射到其中实体的模型。  
  
2.  悬停在该模型之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该模型的 **“常规”** 属性页。  
  
4.  选择 **“点击链接”** 选项卡。  
  
## <a name="options"></a>选项  
 **模型项层次结构**  
 显示模型命名空间中可以为其提供自定义报表的实体、文件夹和项。  
  
 **单个实例报表**  
 指定在用户导航需要单个实例数据的视图时要使用的自定义报表。 单击浏览按钮可以选择要使用的报表。  
  
 **多个实例报表**  
 指定在用户导航需要多个实例数据的视图时要使用的自定义报表。 单击浏览按钮可以选择要使用的报表。  
  
## <a name="see-also"></a>请参阅  
 [发布报表](../../2014/reporting-services/publish-reports.md)  
  
  
