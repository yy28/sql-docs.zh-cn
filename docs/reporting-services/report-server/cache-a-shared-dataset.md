---
title: 缓存共享数据集 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9cdc6e030136e770d79b5730d34b9154ac795668
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274519"
---
# <a name="cache-a-shared-dataset"></a>如何缓存一个共享数据集
  提高性能的一种方法是配置共享数据集的缓存属性。 缓存共享数据集后，会在指定的一段时间内保存查询结果。 第一个向使用该共享数据集的报表发出请求的用户必须等到查询结果和所有处理全部完成后才能查看报表。 以后在缓存期间请求该报表的用户将会体验到性能改进，因为查询和处理已经完成。 还可以指定运行查询的缓存刷新计划，并在指定的缓存过期时间之前一直缓存查询结果。  
  
 运行基于共享数据集或缓存刷新计划的报表的用户创建查询缓存，并且在这两种情况下，缓存是否可用都取决于缓存过期时间选项。  
  
 可缓存的共享数据集类型存在限制。 例如，如果数据根据用户身份而有所不同，或者如果数据是使用请求报表的用户的安全令牌进行检索的，则无法缓存查询结果。 有关详细信息，请参阅[缓存共享数据集 (SSRS)](../../reporting-services/report-server/cache-shared-datasets-ssrs.md) 和 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)。  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>计划缓存报表的过期时间  
  
1.  启动 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  在报表管理器中，导航到要为其设置缓存属性的共享数据集，将鼠标悬停在该项上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。  
  
4.  在左框架中，单击 **“缓存”**。  
  
    > [!NOTE]  
    >  如果看到错误 **“未存储用于运行共享数据集的凭据”**，则缓存共享数据集选项将被禁用。 您需要修改数据源以存储凭据，或修改共享数据集以使用其他确实存储了凭据的数据源。  
  
5.  选择 **“缓存共享数据集”**。  
  
6.  选择缓存在 30 分钟后过期的选项。 还可以选择缓存按指定的计划过期。  
  
7.  单击 **“应用”**。  
  
## <a name="see-also"></a>另请参阅  
 [管理共享数据集](../../reporting-services/report-data/manage-shared-datasets.md)  
  
  
