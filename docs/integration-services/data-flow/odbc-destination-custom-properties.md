---
title: ODBC 目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: efeed5fe9390a9e498e225138522bdc1769a22d6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71292221"
---
# <a name="odbc-destination-custom-properties"></a>ODBC Destination Custom Properties

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  下表介绍了 ODBC 目标的自定义属性。 所有属性都可以从 SSIS 属性表达式设置。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|连接|ODBC 连接|用于访问目标数据库的 ODBC 连接。|  
|BatchSize|Integer|用于大容量加载的批处理的大小。 这是作为批处理加载的行数。 只有在支持按行参数绑定时，该属性才有效。 如果不支持按行参数绑定，则批处理大小为 1。|  
|BindCharColumnAs|Integer（枚举）|此属性确定 ODBC 目标如何绑定具有多字节字符串类型的列，例如 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR。<br /><br /> 可能值为 Unicode (0)，这是将列绑定为 SQL_C_WCHAR；值还可以是 ANSI (1)，这是将列绑定为 SQL_C_CHAR。 默认值为 Unicode (0)。<br /><br /> Unicode 是支持将 CHAR 参数作为宽字符串绑定的大多数 ODBC 3.x 访问接口和 ODBC 2.x 访问接口的最佳选项。 如果您将 Unicode 和 ExposeCharColumnsAsUnicode 选择为 True，则用户无需指定源数据库使用的代码页。<br /><br /> **注意：** 此属性在 **“ODBC 目标编辑器”** 中不可用，但可以使用 **“高级编辑器”** 进行设置。|  
|BindNumericAs|Integer（枚举）|此属性确定 ODBC 目标如何将具有数字数据的列与数据类型 SQL_TYPE_NUMERIC 和 SQL_TYPE_DECIMAL 进行绑定。<br /><br /> 可能值为 Char (0)，这是将列绑定为 SQL_C_CHAR；值还可以是 Numeric (1)，这是将列绑定为 SQL_C_NUMERIC。 默认值为 Char (0)。<br /><br /> **注意：** 此属性在 **“ODBC 目标编辑器”** 中不可用，但可以使用 **“高级编辑器”** 进行设置。|  
|DefaultCodePage|Integer|要用于字符串列的代码页。<br /><br /> **注意：** 此属性在 **“ODBC 目标编辑器”** 中不可用，但可以使用 **“高级编辑器”** 进行设置。|  
|InsertMethod|Integer（枚举）|用于插入数据的方法。 可能的值为逐行 (0) 和批处理 (1)。 默认值为批处理 (1)。<br /><br /> 有关这些选项的更多信息，请参阅 [ODBC 目标](../../integration-services/data-flow/odbc-destination.md)中的“加载选项”。|  
|StatementTimeout|Integer|在无错返回应用程序之前等待 SQL 语句执行的秒数。 默认值为 120。|  
|TableName|String|要插入数据的目标表的名称。|  
|TransactionSize|Integer|单个事务中的插入数。 默认值为 0，这意味着 ODBC 目标在自动提交模式下工作。<br /><br /> 因为 ODBC 连接管理器不支持分布式事务，所以，可以使用 0 以外的其他值来设置此属性。 但是，如果连接管理器的 **RetainSameConnection** 属性设置为 **true** ，则此属性必须设置为 0。<br /><br /> **注意：** 此属性在 **“ODBC 目标编辑器”** 中不可用，但可以使用 **“高级编辑器”** 进行设置。|  
|LobChunkSize|Integer|针对 LOB 列的块大小分配。|  
  
  
