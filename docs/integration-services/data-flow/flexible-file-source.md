---
title: 灵活的文件源 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfilesrc.f1
- sql14.dts.designer.afpextfilesrc.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e396e40f30571969b347c464687321b3b038212
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462533"
---
# <a name="flexible-file-source"></a>灵活的文件源

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

借助“灵活的文件源”组件，SSIS 包可读取各种受支持存储服务中的数据  。
当前支持的存储服务为

- [Azure Blob 存储](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
  
要查看“灵活的文件源”的编辑器，请将“灵活的文件源”拖放到数据流设计器上，然后双击它打开编辑器  。
  
“灵活的文件源”是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组成部分  。  
  
“灵活的文件源编辑器”上提供了以下属性  。

- **文件连接管理器类型：** 指定源连接管理器类型。 然后，从指定的类型中选择一个现成的或新建一个。
- **文件夹路径：** 指定源文件夹路径。
- **文件名：** 指定源文件名称。
- **文件格式：** 指定源文件格式。 支持格式为 Text、Avro、ORC 和 Parquet     。
- **列分隔符字符：** 指定用作列分隔符的字符（不支持多字符分隔符）。
- **作为列名称的第一行：** 指定是否将第一行视为列名称。
- **将文件解压缩：** 指定是否将源文件解压缩。
- **压缩类型：** 指定源文件的压缩格式。 支持格式为 GZIP、DEFLATE 和 BZIP2    。
  
“高级编辑器”上提供了以下属性  。

- **rowDelimiter：** 用于分隔文件中的行的字符。 只能使用一个字符。 默认值为 \r\n  。
- **escapeChar：** 用于转义输入文件内容中的列分隔符的特殊字符。 不能同时指定表的 escapeChar 和 quoteChar。 只能使用一个字符。 无默认值。
- **quoteChar：** 将字符串值用引号括起来的字符。 引号字符内的列和行分隔符将被视为字符串值的一部分。 此属性适用于输入和输出数据集。 不能同时指定表的 escapeChar 和 quoteChar。 只能使用一个字符。 无默认值。
- **nullValue：** 用于表示 null 值的一个或多个字符。 默认值为 \N  。
- **encodingName：** 指定编码名称。 请参阅 [Encoding.EncodingName](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8) 属性。
- **skipLineCount：** 指示从输入文件读取数据时要跳过的非空行数。 如果同时指定了 skipLineCount 和 firstRowAsHeader，则先跳过行，然后从输入文件读取标头信息。
- **treatEmptyAsNull：** 指定是否在从输入文件读取数据时将 null 或空字符串视为 null 值。 默认值为 True  。

指定连接信息后，切换到“列”  页，将源列映射到 SSIS 数据流的目标列。

**ORC/Parquet 文件格式的先决条件**

需通过 Java 来使用 ORC/Parquet 文件格式。
Java 版本的体系结构（32/64 位）应与要使用的 SSIS 运行时的体系结构一致。
已测试以下 Java 版本。

- [Zulu OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE 运行时环境 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

**安装 Zulu OpenJDK**

1. 下载并提取安装 zip 包。
2. 从命令提示符处，运行 `sysdm.cpl`。
3. 在“高级”选项卡上，选择“环境变量”   。
4. 在“系统变量”部分中，选择“新建”   。
5. 输入变量名称 `JAVA_HOME`  。
6. 选择“浏览目录”，导航到已提取的文件夹，然后选择 `jre` 子文件夹  。
   然后选择“确定”，“变量值”将自动进行填充   。
7. 选择“确定”，关闭“新建系统变量”对话框   。
8. 选择“确定”，关闭“环境变量”对话框   。
9. 选择“确定”以关闭“系统属性”对话框   。

**安装 Oracle Java SE 运行时环境**

1. 下载并运行 exe 安装程序。
2. 按照安装程序说明完成安装。
