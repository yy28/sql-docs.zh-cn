---
title: 配置数据收集器的属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dc.datacollectionprop.advanced.f1
- sql12.swb.dc.datacollectionprop.general.f1
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37df9ccdd0bc2b44384bb9fd3d130c8d3bf8ca36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62873432"
---
# <a name="configure-properties-of-a-data-collector"></a>配置数据收集器的属性
  本主题将介绍如何配置数据收集器的属性。  
  
## <a name="data-collection-properties-general-tab"></a>数据收集属性（“常规”选项卡）  
 使用此页可以配置管理数据仓库的设置，并指定所收集数据在上载到数据仓库之前的存储位置。  
  
 **启用数据收集**  
 选择此选项可以启用数据收集。 这与运行 sp_syscollector_enable_collector 存储过程的效果相同。 清除此复选框可禁用数据收集且与运行 sp_syscollector_disable_collector 存储过程的效果相同。  
  
 **Server**  
 显示将承载管理数据仓库的服务器的名称。  
  
 **数据库名称**  
 显示用于管理数据仓库的关系数据库的名称。  
  
 **测试连接**  
 使用在配置数据收集时提供的信息测试到指定的 **服务器** 的连接。  
  
 **缓存目录**  
 指定所收集数据在上载到管理数据仓库之前在系统中的存储目录。 如果未指定 **“缓存目录”** ，数据收集器会尝试查找 %TEMP% 和 %TMP% 环境变量并将两个位置中的一个位置用作临时存储的默认位置。 如果未配置这两个环境变量，则会出现错误并且系统将会提示创建一个缓存目录。  
  
## <a name="data-collection-properties-advanced-tab"></a>数据收集属性（“高级”选项卡）  
 使用此页可以为指向管理数据仓库的连接配置重试设置。  
  
 **上载失败后的重试次数**  
 指定上载失败后重试上载到管理数据仓库的次数。 默认值为 1。  
  
## <a name="see-also"></a>请参阅  
 [管理数据收集](data-collection.md)   
 [配置管理数据仓库 (SQL Server Management Studio)](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
