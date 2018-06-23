---
title: XML 输入文件参考（数据库引擎优化顾问）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7dd0170481a3894334dc01b2974a27ace6b736b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017232"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>XML 输入文件引用（数据库引擎优化顾问）
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问可以使用 XML 输入文件来优化数据库。 此 XML 文件指定要用于优化会话的数据库、表、工作负荷文件或表以及优化选项。 您还可以使用此文件指定一个用户指定的配置来执行“假设”分析。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 输入文件包含 XML 元素（每个元素包含文本或其他用于指定优化会话设置的元素）的层次结构。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 输入文件必须符合格式正确的 XML 的标准，因此所有的元素名称都区分大小写。 使用 Pascal case 来指定元素，即第一个字符大写，随后的所有串连单词的第一个字母都大写。  
  
 所有元素值都必须符合 XML 命名约定。 有关这些约定的详细信息，请参阅 MSDN Library 中的 [XML Textual Content](http://go.microsoft.com/fwlink/?LinkId=7614) 。  
  
 请注意，此参考并非综合性参考。 有关可用于定义 XML 输入的所有元素的信息，请参考 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 架构 (DTASchema.xsd)。  
  
## <a name="xml-declaration"></a>XML 声明  
  
-   [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>DTAXML 根元素  
  
-   [DTAXML 元素&#40;DTA&#41;](dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>DTAInput 元素  
  
-   [DTAInput 元素&#40;DTA&#41;](dtainput-element-dta.md)  
  
-   [服务器元素&#40;DTA&#41;](server-element-dta.md)  
  
-   [工作负荷元素&#40;DTA&#41;](workload-element-dta.md)  
  
-   [TuningOptions 元素&#40;DTA&#41;](tuningoptions-element-dta.md)  
  
-   [配置元素&#40;DTA&#41;](configuration-element-dta.md)  
  
## <a name="server-elements"></a>服务器元素  
  
-   [服务器的名称元素&#40;DTA&#41;](name-element-for-server-dta.md)  
  
-   [服务器的数据库元素&#40;DTA&#41;](database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>工作负荷元素  
  
-   [文件元素&#40;DTA&#41;](file-element-dta.md)  
  
-   [为工作负荷的数据库元素&#40;DTA&#41;](database-element-for-workload-dta.md)  
  
-   [EventString 元素&#40;DTA&#41;](eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>优化选项元素  
  
-   [TuningTimeInMin 元素&#40;DTA&#41;](tuningtimeinmin-element-dta.md)  
  
-   [StorageBoundInMB 元素&#40;DTA&#41;](storageboundinmb-element-dta.md)  
  
-   [TestServer 元素&#40;DTA&#41;](testserver-element-dta.md)  
  
-   [FeatureSet 元素&#40;DTA&#41;](featureset-element-dta.md)  
  
-   [分区元素&#40;DTA&#41;](partitioning-element-dta.md)  
  
-   [DropOnlyMode 元素&#40;DTA&#41;](droponlymode-element-dta.md)  
  
-   [KeepExisting 元素&#40;DTA&#41;](keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation 元素&#40;DTA&#41;](onlineindexoperation-element-dta.md)  
  
-   [DatabaseToConnect 元素&#40;DTA&#41;](databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>配置元素  
  
-   [配置的服务器元素&#40;DTA&#41;](server-element-for-configuration-dta.md)  
  
-   [有关配置的数据库元素&#40;DTA&#41;](database-element-for-configuration-dta.md)  
  
-   [建议元素&#40;DTA&#41;](recommendation-element-dta.md)  
  
-   [创建元素&#40;DTA&#41;](create-element-dta.md)  
  
-   [索引元素&#40;DTA&#41;](index-element-dta.md)  
  
-   [索引的名称元素&#40;DTA&#41;](name-element-for-index-dta.md)  
  
-   [索引的列元素&#40;DTA&#41;](column-element-for-index-dta.md)  
  
-   [列的名称元素&#40;DTA&#41;](name-element-for-column-dta.md)  
  
-   [索引的文件组元素&#40;DTA&#41;](filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>数据库元素  
  
-   [数据库的名称元素&#40;DTA&#41;](name-element-for-database-dta.md)  
  
-   [数据库的架构元素&#40;DTA&#41;](schema-element-for-database-dta.md)  
  
-   [架构的名称元素&#40;DTA&#41;](name-element-for-schema-dta.md)  
  
-   [架构的表元素&#40;DTA&#41;](table-element-for-schema-dta.md)  
  
-   [表的名称元素&#40;DTA&#41;](name-element-for-table-dta.md)  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  