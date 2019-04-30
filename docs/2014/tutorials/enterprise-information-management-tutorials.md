---
title: 企业信息管理教程 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8745dc80-193d-4de0-9f17-ba648ab1e81c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ee7cc12f4fde3a2e5116458034ae3d4a8cc1c13a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313844"
---
# <a name="enterprise-information-management-tutorials"></a>企业信息管理教程
  本节包含通过使用在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中随附的企业信息管理 (EIM) 技术在企业中管理信息的教程。 企业信息管理 (EIM) 提供一组解决方案，使组织能够信任其数据的可信性和一致性，以便组织可以作出关键业务决策。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 具有以下技术，帮助您在企业中实现 EIM 解决方案。  
  
-   SQL Server Integration Services (SSIS)。 SSIS 提供强大的可扩展平台，用于在支持业务工作流、数据仓库或主数据管理的全面的提取、转换和加载 (ETL) 解决方案中集成来自不同源的数据。  
  
-   SQL Server Data Quality Services (DQS)。 通过 DQS，您可以清理、匹配、标准化和丰富数据，以便您可以提供可信的信息来用于商业智能、数据仓库和事务处理工作负荷。  
  
-   SQL Server Master Data Services (MDS)。 MDS 提供一个集中的数据中心，确保信息的完整性和数据的一致性在不同应用程序中是不变的。  
  
 [使用 SSIS、 MDS 和 DQS 一起执行企业信息管理&#91;教程&#93;](../../2014/tutorials/enterprise-information-management-using-ssis-mds-and-dqs-together-[tutorial].md)  
 在本教程中，您将学习如何一起使用 SSIS、MDS 和 DQS 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您将使用 DQS 创建一个包含与供应商数据（元数据）有关的知识的知识库，根据该知识库清理一个 Excel 文件中的数据，并且对数据进行匹配以便标识并删除数据中的重复项。 接下来，您将使用用于 Excel 的 MDS 外接程序将已清理和匹配的数据上载到 MDS。 然后，您通过使用一个 SSIS 解决方案自动化整个过程。  
  
## <a name="see-also"></a>请参阅  
 [企业信息管理-Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=270871)  
  
  
