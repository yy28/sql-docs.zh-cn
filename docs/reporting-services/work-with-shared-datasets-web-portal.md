---
title: 使用共享数据集（Web 门户）| Microsoft Docs
ms.custom: ''
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2641ea84-9343-4e6f-aec1-25339031b163
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 97b787e06c3979e8e41586804164edcccc9cd0a0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971715"
---
# <a name="work-with-shared-datasets---web-portal"></a>使用共享数据集（Web 门户）

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

使用共享数据集，你可以单独管理数据集的设置，使其和报表以及使用它的其他目录项分开。 共享数据集可以与分页报表、移动报表和 KPI 一起使用。

你可以查看和管理 Web 门户中共享数据集的属性。 Web 门户可以将你启动到报表生成器中，以创建或编辑共享数据集。

## <a name="create-a-shared-dataset"></a>创建共享数据集
  
若要创建新的共享数据集，你可以执行以下操作。  
  
1.  从菜单栏中选择“新建”。  
  
2.  选择“数据集”。  
  
    ![ssRSDataset-NewDataset](../reporting-services/media/ssrsdataset-newdataset.png)  
  
3.  这将启动报表生成器，或者提示你下载它。  
  
4.  在“新建报表或数据集”对话框中，选择要用于此数据集的数据源连接。 你可能需要浏览到共享数据源的位置。  
  
5.  选择“创建”。  
  
6.  生成数据集，然后选择左上方的“保存”图标将数据集保存回报表服务器。  
  
## <a name="manage-an-existing-shared-dataset"></a>管理现有共享数据集
  
若要管理现有共享数据集，你可以执行以下操作。  
  
> [!NOTE]
> 如果在文件夹中看不到共享数据集，请确保你正在查看数据集。 你可以从 Web 门户右上方的菜单栏中选择“查看”  。 请确保已选中“数据集”。  
  
1.  选择要管理的数据集旁边的省略号 (…)。  
  
    ![ssRSDataset-Ellipse](../reporting-services/media/ssrsdataset-ellipse.png)  
  
2.  选择“管理”会将你转到编辑屏幕。  
  
    ![ssRSDataset-Manage](../reporting-services/media/ssrsdataset-manage.png)  
  
## <a name="properties"></a>属性
  
在属性屏幕中，你可以更改数据集的“名称”和“描述”。 也可以“删除”、“移动”、“在报表生成器中编辑”、“下载”或“替换”。  
  
![ssRSdataset-Properties](../reporting-services/media/ssrsdataset-properties.png)  
  
## <a name="caching"></a>Caching
  
缓存数据集的数据时，你有多个选项。 只需进行简单选择即可开始操作。  
  
1.  **始终用最新数据运行此报表** 在收到请求时会向数据源发出查询。  
  
2.  **缓存此报表的副本并在可用时使用副本** 会将数据的临时副本放在缓存中，以便用于使用此数据集的项。 由于将从缓存中返回数据（而不是重新运行数据集查询），因此进行缓存通常会提高性能。  
  
![ssRSDataset-Caching1](../reporting-services/media/ssrsdataset-caching1.png)  
  
选择“缓存此报表的副本并在可用时使用副本”时将显示更多选项。  
  
![ssRSDataset-Caching2](../reporting-services/media/ssrsdataset-caching2.png)  
  
### <a name="cache-expiration"></a>缓存过期  
  
你可以控制是要在某段时间后针对共享数据集使缓存过期，还是希望按计划使缓存过期。 你可以使用共享计划。  
  
![ssRSDataset-Caching3](../reporting-services/media/ssrsdataset-caching3.png)  
  
> [!NOTE]
> 设置过期时间并不会刷新缓存。 如果没有缓存刷新计划，将在下次执行数据集时刷新数据。  
  
### <a name="cache-refresh-plans"></a>缓存刷新计划  
  
可以使用“缓存刷新计划”创建使用共享数据集数据的临时副本预加载缓存的计划。 刷新计划包括计划和指定或覆盖参数值的选项。 不能覆盖标记为只读的参数值。 可以创建和使用多个刷新计划。   
  
通过“内容管理员”、“我的报表”和“发布者”这些默认角色分配，你可以添加、删除和更改缓存刷新计划的共享数据集。  
  
应用上面的缓存选项后，可以定义缓存刷新计划。 为此，请选择应用缓存设置后出现的“管理刷新计划”链接。 这会将你转到缓存刷新计划页。   
  
若要创建新的缓存刷新计划，请选择“新建缓存刷新计划”。 然后，可以为该计划输入名称并指定一个计划。 如果数据集定义了参数，这些参数将列出，你可以提供值，除非它们标记为只读。  
  
完成后，你便可以选择“创建缓存刷新计划”。  
  
![ssRSDataset-Caching4](../reporting-services/media/ssrsdataset-caching4.png)  
  
> [!NOTE]
> SQL Server 代理必须处于运行状态才能创建缓存刷新计划。  
  
之后，你可以“编辑”  或“删除”  列出的计划。 仅当选择一个缓存刷新计划时才启用“从现有项新建”选项。 此选项将创建一个新的刷新计划，该计划是从原始计划复制而来。 将打开缓存刷新计划页，其中预先填充了所选计划的详细信息。 然后，您可以修改刷新计划选项并用新说明保存该计划。  

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
