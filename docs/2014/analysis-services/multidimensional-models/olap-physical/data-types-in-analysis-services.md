---
title: Analysis Services 中的数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 910be4f4-3010-41cd-9fdc-f0a79a0ce823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ecdc64918e582f25f0e017d263c66e78c0d1bee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62725381"
---
# <a name="data-types-in-analysis-services"></a>Analysis Services 中的数据类型
  对于所有<xref:Microsoft.AnalysisServices.DataItem>对象， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持的以下子集`System.Data.OleDb.OleDbType`。 若要设置或读取数据类型，请使用[DataItem 数据类型 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl)。  
  
## <a name="supported-data-types"></a>支持的数据类型  
  
|||  
|-|-|  
|BigInt|64 位有符号整数。 *BigInt*值类型表示其值范围从负9223372036854775808到正9223372036854775807的整数。|  
|Binary|**Byte**类型的二进制数据的流。 **Byte**是一种值类型，它表示值介于0到255之间的无符号整数。|  
|Boolean|此类型的实例具有 `true` 或 `false` 值。|  
|货币|一个*货币*值，范围为-922337203685477.5808 到 + 922337203685477.5807，精确到货币单位的万分之一（四位数）。|  
|Date|以双精度存储的日期和时间数据。 整数部分是自 1899 年 12 月 30 日以来的天数，而小数部分是不足一天的部分或一天中的某个时间。|  
|Double|浮点数，范围在 -1.79769313486232E +308 到 1.79769313486232E +308 之间。 Double 值存储精度最高为 15 个小数位的数字信息。|  
|Integer|32 位有符号整数，表示其值范围在负的 2,147,483,648 到正的 2,147,483,647 之间的有符号整数。|  
|Single|浮点数，范围在 - 3.4028235E +38 到 3.4028235E +38 之间。 Single 值存储精度最高为 7 个小数位的数字信息。|  
|Smallint|16 位有符号整数。 *Smallint*值类型表示其值范围从负32768到正32767的带符号整数。|  
|Tinyint|一个 8 位有符号整数。 Tinyint 值类型表示其值范围从负的 128 到正的 127 的整数。|  
|UnsignedBigInt|一个 64 位无符号整数。 *UnsignedBigInt*值类型表示其值范围从0到18446744073709551615的无符号整数。|  
|UnsignedInt|32 位无符号整数。 *UnsignedInt*值类型表示其值范围从0到4294967295的无符号整数。|  
|UnsignedSmallInt|16 位无符号整数。 *UnsignedSmallInt*值类型表示其值范围从0到65535的无符号整数。|  
|UnsignedTinyInt|8 位无符号整数。 *UnsignedTinyInt*值类型表示其值介于0到255之间的无符号整数|  
|WChar|Unicode 字符的以 Null 值结束的流。 *WChar*是用于表示文本的 Unicode 字符的有序集合。|  
  
## <a name="amo-validations-on-data-types"></a>针对数据类型的 AMO 验证  
 下表列出了分析管理对象 (AMO) 针对特定绑定执行的附加验证：  
  
|Object|绑定|允许的数据类型|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|所有（Binary 除外）|  
||NameColumn|仅 WChar|  
||SkippedLevelsColumn|仅 integer 类型：BigInt、Integer、SmallInt、TinyInt、UnsignedBigInt、UnsignedInt、UnsignedSmallInt、UnsignedTinyInt|  
||CustomRollupColumn|仅 WChar|  
||CustomRollupPropertiesColumn|仅 WChar|  
||UnaryOperatorColumn|仅 WChar|  
||ValueColumn|All|  
|AttributeTranslation|CaptionColumn|仅 WChar|  
|ScalarMiningStructureColumn|KeyColumns|所有（Binary 除外）|  
||NameColumn|仅 WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|所有（Binary 除外）|  
|MeasureGroupAttribute|KeyColumns|所有（Binary 除外）|  
|非重复计数度量值|源|BigInt、Currency、Double、Integer、Single、SmallInt、TinyInt、UnsignedBigInt、UnsignedInt、UnsignedSmallInt、UnsignedTinyInt|  
  
  
