---
title: Azure SQL DW 上传任务 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPDWUPTASK.F1
- SQL11.DTS.DESIGNER.AFPDWUPTASK.F1
ms.assetid: 112cf764-f85a-4c1a-b732-d299d717c0d4
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1e5e39f8049a5f2832e7a37381c4d22ef2483b62
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62836374"
---
# <a name="azure-sql-dw-upload-task"></a>Azure SQL DW 上传任务
“Azure SQL DW 上传任务”  使 SSIS 包可将本地数据上传到 Azure SQL 数据仓库 (DW) 中的表。 当前支持的源数据文件格式是采用 UTF8 编码的带分隔符的文本。 上传过程将按照高效的 PolyBase 方法。 具体而言，数据首先将上传到 Azure Blob 存储，然后上传到 Azure SQL DW。 因此，需要 Azure Blob 存储帐户才可使用此任务。

若要添加“Azure SQL DW 上传任务” ，请将其从 SSIS 工具栏拖放到设计器画布中，双击或右键单击它，然后单击“编辑”  ，查看任务编辑器对话框。

在“常规”  页上配置以下属性。

字段|Description
-----|-----------
LocalDirectory|指定包含待上传数据文件的本地目录。
Recursively|指定是否以递归方式搜索子目录。
FileName|指定用于选择具有特定名称模式的文件的名称筛选器。 例如 MySheet\*.xls\* 将包含如 MySheet001.xsl 和 MySheetABC.xslx 等文件。
RowDelimiter|指定标记每一行末尾的字符。
ColumnDelimiter|指定标记每一列末尾的一个或多个字符。 例如 |（管道）、\t（制表符）、'（单引号），"（双引号）以及 0x5c（反斜杠）。
IsFirstRowHeader|指定每个数据文件的第一行是否包含列名称，而非实际数据。
AzureStorageConnection|指定 Azure 存储连接管理器。
BlobContainer|指定通过 PolyBase 将本地数据上传并转送到 Azure DW 的目标 blob 容器名称。 如果此容器不存在，则将创建新容器。
BlobDirectory|指定通过 PolyBase 将本地数据上传并转送到 Azure DW 的目标 blob 目录（虚拟层次结构）。
RetainFiles|指定是否保留已上传到 Azure 存储的文件。
CompressionType|指定将文件上传到 Azure 存储时使用的压缩格式。 本地源不受影响。
CompressionLevel|指定用于压缩格式的压缩级别。
AzureDwConnection|指定 Azure SQL DW 的 ADO.NET 连接管理器。
TableName|指定目标表的名称。 可选择现有的表名称，或通过选择“\<新建表...>”创建一个新表。
TableDistribution|指定新表的分发方法。 已为 **TableName**指定新的表名称时适用。
HashColumnName|指定用于哈希表分发的列。 已为 **TableDistribution** 指定 **HASH**时适用。

根据是上传到新表还是现有表，看到的“映射”  页面会有所不同。 如果是前者，请在待创建目标表中配置要映射到的源列及其对应名称。 如果是后者，请配置源和目标列之间的映射关系。

在“列”  页上，配置每个源列的数据类型属性。

“T-SQL”  页显示用于将数据从 Azure Blob 存储加载到 Azure SQL DW 的 T-SQL。 T-SQL 从其他页面的配置中自动生成，并在任务执行的过程中执行。 若要满足特定需求，可通过单击“编辑”  按钮选择手动编辑已生成的 T-SQL。 之后可单击“重置”  按钮还原为自动生成的 T-SQL。
