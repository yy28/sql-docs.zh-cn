---
title: 保护共享数据集项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 08e6d8b5-d88c-4ed2-9c05-55c757e00014
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 29b3430e4a29130c4189fbce1a9a023b7a7f26da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101641"
---
# <a name="secure-shared-dataset-items"></a>保护共享数据集项
  在报表服务器上，共享数据集项可由多个报表使用。 您可以对共享数据集加以保护以便控制用户能够访问的程度。 默认情况下，只有是“管理员”内置组的成员的用户才能查看共享数据集、修改属性、启用缓存、创建缓存刷新计划以及删除项。 所有其他用户必须具有为其创建的角色分配才能访问共享数据集。  
  
 若要设置安全性，应创建相应的角色分配，以指定对共享数据集拥有访问权限的用户帐户或组帐户。  
  
## <a name="role-based-access-to-shared-datasets"></a>对共享数据集的基于角色的访问  
 为了授予对共享数据集的访问权限，您可以允许用户从父文件夹继承现有的角色分配，也可以针对项本身创建新的角色分配。  
  
 通过“内容管理员”、“我的报表”和“发布者”默认角色分配，您可以添加、删除和编辑项属性，以及查看缓存数据集的相关报表和共享数据源。 若要编辑共享数据集定义，可使用默认角色分配“报表生成者”或“内容管理员”。  
  
 因为角色分配通常从父节点继承，所以，启用了“查看报表”  任务的文件夹可以将该权限传递给该文件夹中的共享数据集和报表。  
  
 若要对共享数据集及其查询结果提供更多的控制，请对共享数据集项配置项级安全性，或者将共享数据集保存到某一文件夹，然后对该文件夹配置项级安全性。  
  
## <a name="shared-dataset-parameters"></a>共享数据集参数  
 共享数据集参数不能用于限制特定用户的数据。 共享数据集参数旨在提供一种方法，以便指定对共享数据集进行处理时要包括的数据。 在报表服务器上，不能保护共享数据集参数的值。  
  
 在共享数据集定义中，您可以将参数标记为只读并指定默认值。 在服务器上不能覆盖标记为只读的参数。 例如，在针对某一共享数据集的缓存刷新计划中，不能为只读参数指定值。 如果这些共享数据集参数包括引用用户全局集合的表达式，或者具有任何其他用户依赖关系，则不能为该共享数据集创建缓存刷新计划。  
  
## <a name="tasks-access-to-items-and-default-roles"></a>任务、对项的访问和默认角色  
 共享数据集采用与报表相同的安全模型。 若要向用户提供针对特定操作的权限，请选择一个角色，该角色包含具备这些权限的相应任务。 下表列出了任务和它们包含的操作。  
  
|选择此任务|授权用户以下权限|包含该任务的默认角色|  
|----------------------|---------------------------------|-----------------------------------------|  
|查看报表|在文件夹层次结构中查看共享数据集项。 如果不包含此任务，则用户将无法查看项，并且用户可能无法认识到该数据集可用。|浏览者<br /><br /> 内容管理员<br /><br /> 报表生成器<br /><br /> 我的报表|  
|管理报表|查看用于指定名称、说明和连接信息的属性。 此任务还用于在文件夹层次结构中显示共享数据集项。 如果选择此任务，则可以省略“查看报表”任务。|内容管理员<br /><br /> 发布服务器<br /><br /> 我的报表|  
|使用报表|查看共享数据集定义。|内容管理员<br /><br /> 报表生成器|  
|设置项的安全性|创建和修改控制共享数据集访问权限的角色分配。 此任务必须与“查看报表”或“管理报表”任务一起使用。 否则，由于用户无法选择项，此任务将不会发挥任何作用。|内容管理员|  
  
 有关详细信息，请参阅 [项级任务](tasks-and-permissions-item-level-tasks.md) 和 [预定义角色](role-definitions-predefined-roles.md)。  
  
## <a name="see-also"></a>请参阅  
 [管理共享数据集](../report-data/manage-shared-datasets.md)   
 [保护文件夹](secure-folders.md)   
 [保护报表和资源](secure-reports-and-resources.md)   
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)   
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)  
  
  
