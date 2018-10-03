---
title: 处理和存储位置 （分区向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a1462a2cc1338e973df3d0fd84641aa24d0bc41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198617"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>处理位置和存储位置（分区向导）
  可以使用 **“处理位置和存储位置”** 页，指定拥有分区的多维数据集的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例以及存储分区数据的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。 通过指定远程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例或指定默认存储位置之外的其他存储位置，可以将分区定义为远程分区。 有关远程分区的详细信息，请参阅 [远程分区](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)。  
  
## <a name="processing-location-options"></a>处理位置选项  
 **当前服务器实例**  
 将当前 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例设置为负责处理该分区。  
  
 **远程 Analysis Services 数据源**  
 设置一个远程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例来负责处理此分区。  
  
 从下拉列表中，选择代表负责处理该分区的远程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的数据源。  
  
> [!NOTE]  
>  如果在所选择的数据源中为 `Initial Catalog` 连接字符串属性设置的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库无效，或者在 `Initial Catalog` 连接字符串属性中指定的数据库不支持远程分区（换句话说，为指定数据库的 `MasterDatasourceID` 属性设置的值无效），则将发生错误。  
  
 **新建**  
 创建一个新的数据源，代表负责处理该分区的远程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。  
  
## <a name="storage-location-options"></a>存储位置选项  
 **默认服务器位置**  
 将当前 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的数据文件夹设置为分区的聚合和索引数据的存储位置。  
  
 **指定的文件夹**  
 指定分区的聚合和索引数据的存储位置。  
  
 **...**  
 显示“查找远程文件夹”对话框，在该对话框中可以为“指定的文件夹”选择文件夹。  
  
## <a name="see-also"></a>请参阅  
 [分区向导的 F1 帮助&#40;Analysis Services-多维数据&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [分区&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [查找远程文件夹对话框&#40;Analysis Services-多维数据&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  
