---
title: 结论 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: b1e6fde6-c3a7-4b91-b176-fa465325dd21
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4159972e7b72dde9a3ba47125ac9b8eae568c64
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210477"
---
# <a name="conclusion"></a>结语
  在本教程中，您已学习了如何一起使用 SQL Server Integration Services (SSIS)、Master Data Services (MDS) 和 Data Quality Services (DQS) 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您使用数据质量客户端工具创建了一个包含与供应商有关知识的 DQS 知识库，对照该知识库清理了一个 excel 文件中的输入供应商数据，然后通过使用该知识库中的匹配策略对供应商数据进行了匹配，以便标识并删除数据中的重复项。 接下来，通过使用用于 Excel 的 MDS 外接程序，您将已清理和已匹配的供应商列表存储到 MDS 中。 最后，您通过创建一个 SSIS 解决方案，将接收输入数据、清理和匹配数据以及将主数据存储于 MDS 中的整个过程自动化。  
  
## <a name="for-more-information"></a>详细信息：    
  
 [企业信息管理 (EIM): 一起将 SSIS、 DQS 和 MDS （视频）](http://go.microsoft.com/fwlink/?LinkId=258672)  
  
  
