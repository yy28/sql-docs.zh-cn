---
title: XML 输入文件参考（数据库引擎优化顾问）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b560b36eb98ec73723a4ce25cb3c647f4962b634
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62509979"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>XML 输入文件引用（数据库引擎优化顾问）
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问可以使用 XML 输入文件来优化数据库。 此 XML 文件指定要用于优化会话的数据库、表、工作负荷文件或表以及优化选项。 您还可以使用此文件指定一个用户指定的配置来执行“假设”分析。  
  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 输入文件包含 XML 元素（每个元素包含文本或其他用于指定优化会话设置的元素）的层次结构。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 输入文件必须符合格式正确的 XML 的标准，因此所有的元素名称都区分大小写。 使用 Pascal case 来指定元素，即第一个字符大写，随后的所有串连单词的第一个字母都大写。  
  
 所有元素值都必须符合 XML 命名约定。 有关这些约定的详细信息，请参阅 MSDN Library 中的 [XML Textual Content](https://go.microsoft.com/fwlink/?LinkId=7614) 。  
  
 请注意，此参考并非综合性参考。 有关可用于定义 XML 输入的所有元素的信息，请参考 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问 XML 架构 (DTASchema.xsd)。  
  
## <a name="xml-declaration"></a>XML 声明  
  
-   [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>DTAXML 根元素  
  
-   [&#40;DTA&#41;的 DTAXML 元素](dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>DTAInput 元素  
  
-   [&#40;DTA&#41;的 DTAInput 元素](dtainput-element-dta.md)  
  
-   [服务器元素 (DTA)](server-element-dta.md)  
  
-   [&#40;DTA&#41;的工作负荷元素](workload-element-dta.md)  
  
-   [&#40;DTA&#41;的 TuningOptions 元素](tuningoptions-element-dta.md)  
  
-   [配置元素 &#40;DTA&#41;](configuration-element-dta.md)  
  
## <a name="server-elements"></a>服务器元素  
  
-   [服务器 &#40;DTA&#41;的名称元素](name-element-for-server-dta.md)  
  
-   [Server &#40;DTA&#41;的数据库元素](database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>工作负荷元素  
  
-   [&#40;DTA&#41;的文件元素](file-element-dta.md)  
  
-   [用于工作负荷 &#40;DTA&#41;的数据库元素](database-element-for-workload-dta.md)  
  
-   [&#40;DTA&#41;的 EventString 元素](eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>优化选项元素  
  
-   [&#40;DTA&#41;的 TuningTimeInMin 元素](tuningtimeinmin-element-dta.md)  
  
-   [&#40;DTA&#41;的 StorageBoundInMB 元素](storageboundinmb-element-dta.md)  
  
-   [&#40;DTA&#41;的 TestServer 元素](testserver-element-dta.md)  
  
-   [&#40;DTA&#41;的 FeatureSet 元素](featureset-element-dta.md)  
  
-   [&#40;DTA&#41;分区元素](partitioning-element-dta.md)  
  
-   [&#40;DTA&#41;的 DropOnlyMode 元素](droponlymode-element-dta.md)  
  
-   [&#40;DTA&#41;的 KeepExisting 元素](keepexisting-element-dta.md)  
  
-   [&#40;DTA&#41;的 OnlineIndexOperation 元素](onlineindexoperation-element-dta.md)  
  
-   [&#40;DTA&#41;的 DatabaseToConnect 元素](databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>配置元素  
  
-   [用于配置 &#40;DTA&#41;的服务器元素](server-element-for-configuration-dta.md)  
  
-   [用于配置 &#40;DTA&#41;的数据库元素](database-element-for-configuration-dta.md)  
  
-   [DTA&#41;&#40;建议元素](recommendation-element-dta.md)  
  
-   [&#40;DTA&#41;创建元素](create-element-dta.md)  
  
-   [Index 元素 &#40;DTA&#41;](index-element-dta.md)  
  
-   [用于索引 &#40;DTA&#41;的名称元素](name-element-for-index-dta.md)  
  
-   [用于索引 &#40;DTA&#41;的列元素](column-element-for-index-dta.md)  
  
-   [&#40;DTA&#41;的列的名称元素](name-element-for-column-dta.md)  
  
-   [用于索引 &#40;DTA&#41;的文件组元素](filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>数据库元素  
  
-   [数据库的名称元素 (DTA)](name-element-for-database-dta.md)  
  
-   [数据库的架构元素 (DTA)](schema-element-for-database-dta.md)  
  
-   [架构 &#40;DTA&#41;的名称元素](name-element-for-schema-dta.md)  
  
-   [架构 &#40;DTA&#41;的 Table 元素](table-element-for-schema-dta.md)  
  
-   [用于&#41;DTA 的表 &#40;名称元素](name-element-for-table-dta.md)  
  
## <a name="see-also"></a>另请参阅  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
