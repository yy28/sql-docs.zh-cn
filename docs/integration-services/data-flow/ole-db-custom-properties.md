---
title: OLE DB 自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 039b36c2092d9e08e81802e441f42587be66445c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298152"
---
# <a name="ole-db-custom-properties"></a>OLE DB 自定义属性

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **源自定义属性**  
  
 OLE DB 源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍 OLE DB 源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用来访问数据库的模式。 可能的值包括： **“打开行集”** 、 **“从变量打开行集”** 、 **“SQL 命令”** 和 **“变量中的 SQL 命令”** 。 默认值为 **“打开行集”** 。|  
|AlwaysUseDefaultCodePage|Boolean|一个值，指示是使用每列的 **DefaultCodePage** 属性的值，还是尝试从每列的区域设置中派生代码页。 此属性的默认值为 **False**。|  
|CommandTimeout|Integer|命令超时之前的秒数。如果值为 0，则表示无限期超时。<br /><br /> 注意：此属性未在 OLE DB 源编辑器中提供，但可以使用“高级编辑器”进行设置   。|  
|DefaultCodePage|Integer|当无法从数据源使用代码页信息时所使用的代码页。|  
|OpenRowset|String|用来打开行集的数据库对象的名称。|  
|OpenRowsetVariable|String|该变量包含用来打开行集的数据库对象的名称。|  
|ParameterMapping|String|从 SQL 命令中的参数到变量的映射。|  
|SqlCommand|String|要执行的 SQL 命令。|  
|SqlCommandVariable|String|包含要执行的 SQL 命令的变量。|  
  
 OLE DB 源的输出和输出列没有自定义属性。  
  
 有关详细信息，请参阅 [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)。  
  
 **目标自定义属性**  
  
 OLE DB 目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍 OLE DB 目标的自定义属性。 所有属性均可读/写。  
  
> [!NOTE]  
>  此处列出的 FastLoad 选项（FastLoadKeepIdentity、FastLoadKeepNulls 和 FastLoadOptions）对应于由 Microsoft OLE DB Provider for SQL Server (SQLOLEDB) 实现的 **IRowsetFastLoad** 接口公开的具有相似名称的属性。 有关详细信息，请在 MSDN 库中搜索 IRowsetFastLoad。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer（枚举）|一个指定目标如何访问其目标数据库的值。<br /><br /> 此属性可以具有下列值之一：<br /><br /> <br /><br /> “OpenRowset”(0) - 需要提供表或视图的名称  。<br /><br /> “OpenRowset from Variable”(1) - 需要提供包含表或视图名称的变量的名称  。<br /><br /> “OpenRowset Using Fastload” (3) - 需要提供表或视图名称  。<br /><br /> “OpenRowset Using Fastload from Variable”(4) - 需要提供包含表或视图名称的变量的名称  。<br /><br /> “SQL 命令”(2) - 需要提供 SQL 语句  。|  
|AlwaysUseDefaultCodePage|Boolean|一个值，指示是使用每列的 **DefaultCodePage** 属性的值，还是尝试从每列的区域设置中派生代码页。 此属性的默认值为 **False**。|  
|CommandTimeout|Integer|SQL 命令在超时前可以运行的最大秒数。如果值为 0，则表示不限制时间。 此属性的默认值为 0。<br /><br /> 注意：此属性未在 OLE DB 目标编辑器中提供，但可以使用“高级编辑器”进行设置   。|  
|DefaultCodePage|Integer|与 OLE DB 目标关联的默认代码页。|  
|FastLoadKeepIdentity|Boolean|该值指定加载数据时是否复制标识值。 此属性仅对其中一个快速加载选项可用。 此属性的默认值为 **False**。 此属性对应 OLE DB [IRowsetFastLoad (OLE DB)](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 属性 **SSPROP_FASTLOADKEEPIDENTITY**。|  
|FastLoadKeepNulls|Boolean|一个值，指定加载数据时是否复制 Null 值。 此属性仅对其中一个快速加载选项可用。 此属性的默认值为 **False**。 此属性对应 OLE DB [IRowsetFastLoad (OLE DB)](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 属性 **SSPROP_FASTLOADKEEPNULLS**。|  
|FastLoadMaxInsertCommitSize|Integer|一个值，指定 OLE DB 目标在快速加载操作期间尝试提交的批大小。 默认值 **0**指示处理所有的行后的单个提交操作。|  
|FastLoadOptions|String|快速加载选项的集合。 快速加载选项包括锁定表和检查约束。 可以指定其中的一个，或同时指定两个，或不指定其中的任何一个。 此属性对应 OLE DB IRowsetFastLoad 属性 **SSPROP_FASTLOADOPTIONS** 并接受字符串选项，如 **CHECK_CONSTRAINTS** 和 **TABLOCK**。<br /><br /> 注意：此属性的某些选项未在 Excel 目标编辑器  中提供，但可以使用“高级编辑器”  进行设置。|  
|OpenRowset|String|当 AccessMode 为 **OpenRowset**时，OLE DB 目标访问的表或视图的名称。|  
|OpenRowsetVariable|String|当 AccessMode 为 **OpenRowset from Variable**时，包含 OLE DB 目标访问的表或视图名称的变量的名称。|  
|SqlCommand|String|当 AccessMode 为 **SQL 命令**时，OLE DB 目标用于指定数据的目标列的 Transact-SQL 语句。|  
  
 OLE DB 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
