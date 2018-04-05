---
title: XML 输入文件引用 （数据库引擎优化顾问） |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d507c858f2103af6521e57ffca3385a23c913cd2
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>XML 输入文件引用（数据库引擎优化顾问）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问可以使用 XML 输入的文件优化数据库。 此 XML 文件指定要用于优化会话的数据库、表、工作负荷文件或表以及优化选项。 您还可以使用此文件指定一个用户指定的配置来执行“假设”分析。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 输入文件包含 XML 元素（每个元素包含文本或其他用于指定优化会话设置的元素）的层次结构。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 输入文件必须符合格式正确的 XML 的标准，因此所有的元素名称都区分大小写。 使用 Pascal case 来指定元素，即第一个字符大写，随后的所有串连单词的第一个字母都大写。  
  
 所有元素值都必须符合 XML 命名约定。 有关这些约定的详细信息，请参阅 MSDN Library 中的 [XML Textual Content](http://go.microsoft.com/fwlink/?LinkId=7614) 。  
  
 请注意，此参考并非综合性参考。 有关可用于定义 XML 输入的所有元素的信息，请参考 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 架构 (DTASchema.xsd)。  
  
## <a name="xml-declaration"></a>XML 声明  
  
-   [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>DTAXML 根元素  
  
-   [DTAXML 元素 &#40; DTA &#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>DTAInput 元素  
  
-   [DTAInput 元素 &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [服务器元素 &#40; DTA &#41;](../../tools/dta/server-element-dta.md)  
  
-   [工作负荷元素 &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)  
  
-   [TuningOptions 元素 &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [配置元素 &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>服务器元素  
  
-   [服务器 &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-server-dta.md)  
  
-   [服务器 &#40; DTA &#41; 的数据库元素](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>工作负荷元素  
  
-   [文件元素 &#40; DTA &#41;](../../tools/dta/file-element-dta.md)  
  
-   [工作负荷 &#40; DTA &#41; 的数据库元素](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [EventString 元素 &#40; DTA &#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>优化选项元素  
  
-   [TuningTimeInMin 元素 &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [StorageBoundInMB 元素 &#40; DTA &#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [TestServer 元素 &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet 元素 &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [分区元素 &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [DropOnlyMode 元素 &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting 元素 &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation 元素 &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [DatabaseToConnect 元素 &#40; DTA &#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>配置元素  
  
-   [用于 Configuration &#40; DTA &#41; 的服务器元素](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Configuration &#40; DTA &#41; 的数据库元素](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [建议元素 &#40; DTA &#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [创建元素 &#40; DTA &#41;](../../tools/dta/create-element-dta.md)  
  
-   [索引元素 &#40; DTA &#41;](../../tools/dta/index-element-dta.md)  
  
-   [索引 &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-index-dta.md)  
  
-   [索引 &#40; DTA &#41; 的列元素](../../tools/dta/column-element-for-index-dta.md)  
  
-   [列 &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-column-dta.md)  
  
-   [索引 &#40; DTA &#41; 的文件组元素](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>数据库元素  
  
-   [数据库 &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-database-dta.md)  
  
-   [数据库 &#40; DTA &#41; 的架构元素](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [架构 &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [架构 &#40; DTA &#41; 的表元素](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Table &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
