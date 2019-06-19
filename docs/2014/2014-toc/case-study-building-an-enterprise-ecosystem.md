---
title: 案例研究：构建一个企业生态系统与 Microsoft Dynamics ERP 和 SQL Server 2014 复制的可伸缩性和性能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 2b0b5ab7-4e08-431a-bd59-360177c4565c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64a1423295b8117640de555a7132a44af98b87c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470098"
---
# <a name="case-study-building-an-enterprise-ecosystem-with-microsoft-dynamics-erp-and-sql-server-2014-replication-for-scalability-and-performance"></a>案例研究：使用 Microsoft Dynamics ERP 和 SQL Server 2014 复制构建一个企业生态系统以实现可伸缩性并提高性能

  **摘要：** 本文介绍了以下方案：  
如何在 SQL Server 2014 中使用事务复制，可跨多个节点分发 Dynamics AX 客户端从事务。 因为数据以实时的方式在节点上进行维护，因此事务复制提供了数据冗余，可用于提高数据的可用性，其中包括适用于更加高效的性能分析的数据。  
如何在利用事务复制时了解涉及的具体内容，以在 Microsoft Dynamics ERP 中构建高度可伸缩的企业生态系统。 提供高性能和可伸缩性，无需自定义 AX 自带功能。  
  
 事务复制通常用于需要高吞吐量的服务器到服务器工作流中。 其中包括如下方案：提高可伸缩性和可用性、数据仓库和报告、集成多个站点的数据、集成异类数据以及减轻批处理的负荷。 本白皮书介绍了在 Microsoft Dynamics ERP 中利用事务复制的不同方案和关联模式。 它还介绍了在考虑使用事务复制构建特定于企业资源规划 (ERP) 的企业解决方案时所面临的挑战和最佳做法，以及不同阶段的性能分析。  
  
 此内容是适用于开发人员、架构师和数据库管理员。 假定本白皮书的读者具有 SQL Server 2008、2012 或 2014 的基本知识以及 SQL Server 的管理经验。  
  
 **作者：** Prabhakaran Sethuraman (PRAB)，Microsoft  
  
 **技术审阅人员：** Prabhakaran Sethuraman (PRAB)，Microsoft;Santosh Padhy，Microsoft;Pavel Majstrov，Microsoft;Karthik Sankaranarayanan，Microsoft;Jon Acone，Microsoft;David Stahlkopf，Microsoft;Kent Oldenburger，Microsoft;Mandi Ohlinger，Microsoft;Jason Roth Microsoft  
  
 **发布时间**：2015 年 10 月  
  
 **适用于**：SQL Server 2008、SQL Server 2012 和 SQL Server 2014  
  
 若要查看该文档，请下载  
        [案例研究：构建使用 Microsoft Dynamics ERP 和 SQL Server 2014 Replication 一个企业生态系统的可伸缩性和性能](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/A%20Case%20Study%20Using%20Replication%20to%20Build%20an%20Enterprise%20Ecosystem%20in%20Microsoft%20Dynamics%20ERP%20for%20Scalability%20and%20Performance.docx)Word 文档。  
  
  
