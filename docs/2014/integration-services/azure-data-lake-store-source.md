---
title: Azure Data Lake Store 源 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1a8f60cbdf2653a3d582544a487e71e62168929
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388545"
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 源
  “Azure Data Lake Store 源”  组件允许 SSIS 包读取 Azure Data Lake Store 中的数据。 支持的文件格式为：文本和 Avro。
  
## <a name="configure-the-azure-data-lake-store-source"></a>配置 Azure Data Lake Store 源 
  
1.  若要查看 Azure Data Lake Store 源的编辑器，请将“Azure Data Lake Store 源”  拖放到数据流设计器上，然后双击打开编辑器。  
  
2.  对于“Azure Data Lake Store 连接管理器”  字段，请指定一个现有的 Azure Data Lake Store 连接管理器，或新建一个引用 Azure Data Lake Store 服务的连接管理器。  
  
    1.  对于“文件路径”  字段，请指定 Azure Data Lake Store 中源文件的文件路径。   
  
    2.  对于“文件格式”  字段，请指定源文件的文件格式。  
  
        如果文件格式是文本，则必须指定“列分隔符字符”  值。 此外，如果文件中的第一行包含列名称，请选择“在第一个数据行中显示列名称”  。  
  
3.  指定连接信息后，切换到“列”  页，将源列映射到 SSIS 数据流的目标列。  
