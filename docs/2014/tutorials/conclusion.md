---
title: 结论 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b1e6fde6-c3a7-4b91-b176-fa465325dd21
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0c816aea527a9cf667d96c323249a572d756b3d6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025318"
---
# <a name="conclusion"></a>结束语
  在本教程中，您已学习了如何一起使用 SQL Server Integration Services (SSIS)、Master Data Services (MDS) 和 Data Quality Services (DQS) 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您使用数据质量客户端工具创建了一个包含与供应商有关知识的 DQS 知识库，对照该知识库清理了一个 excel 文件中的输入供应商数据，然后通过使用该知识库中的匹配策略对供应商数据进行了匹配，以便标识并删除数据中的重复项。 接下来，通过使用用于 Excel 的 MDS 外接程序，您将已清理和已匹配的供应商列表存储到 MDS 中。 最后，您通过创建一个 SSIS 解决方案，将接收输入数据、清理和匹配数据以及将主数据存储于 MDS 中的整个过程自动化。  
  
## <a name="for-more-information"></a>详细信息：    
  
 [企业信息管理 (EIM):组合在一起 SSIS、 DQS 和 MDS （视频）](https://go.microsoft.com/fwlink/?LinkId=258672)  
  
  
