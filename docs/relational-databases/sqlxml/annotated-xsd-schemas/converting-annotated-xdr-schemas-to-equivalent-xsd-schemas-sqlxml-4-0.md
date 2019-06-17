---
title: 转换带批注的 XDR 架构为等效的 XSD 架构 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71c2f79ae39ff8617d491d015db7eecb23647d30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678024"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>将带批注的 XDR 架构转换为等效的 XSD 架构 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 架构定义 (XSD) 语言是精简 XML 数据 (XDR) 架构定义语言的后继版本。 随着在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中引入对 XSD 的支持，它假定新的带批注的架构是使用 XSD 创建的。 SQLXML 4.0 包括一个 XDR 到 XSD 转换器工具，此工具旨在帮助您将现有带批注的 XDR 架构转换为等效的 XSD 架构。  
  
> [!IMPORTANT]  
>  仅当要将带批注的 XDR 架构转换为 XSD 以与 SQLXML 4.0 一起使用时才应使用此工具。 这并不是通用 XDR 到 XSD 转换器工具。 在其他环境中使用转换的 XSD 架构时，其行为可能与原始 XDR 架构的行为有所不同。  
  
 如果输入 XDR 文件在 XML 声明中指定了编码，这将成为生成的 XSD 输出文件的编码。  
  
 转换器工具 (Cvtschema.exe) 安装在 Program Files\SQLXML 4.0\bin 文件夹中，并在命令提示符下执行。  
  
 常规语法如下：  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 其中：  
  
 XDRFileName  
 为要转换为 XSD 的 XDR 文件的名称。 此工具将读取输入 XDR 文件，并在当前工作目录中创建 XSD 输出文件。 如果输入文件具有 .xdr 或 .xml 扩展名，则将使用相同的名称但使用 .xsd 扩展名创建输出 XSD 文件。 如果输入的文件扩展名是.xml 或.xdr （或以外的扩展名是缺失），输出文件创建具有相同名称和.xsd 扩展名追加到输入的文件的名称。 例如，如果输入 XDR 文件名为 SampleFile.abc，则生成的 XSD 将保存为 SampleFile.abc.xsd。  
  
 -y  
 （可选）用转换器工具生成的 XSD 文件覆盖现有 XSD 文件。 如果未指定此标志，则此工具将提示您指定是否要覆盖现有 XSD 文件，并且您可以选择更改输出文件名。  
  
 -w  
 （可选）返回在转换过程中由此工具生成的一般警告。 默认情况下，此工具仅为致命错误显示消息。  
  
 -?  
 返回您可以使用指定的选项的列表**cvtschema**，以及解释。  
  
## <a name="see-also"></a>请参阅  
 [XSD 数据类型映射到 XPath 数据类型&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [XSD 批注&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
