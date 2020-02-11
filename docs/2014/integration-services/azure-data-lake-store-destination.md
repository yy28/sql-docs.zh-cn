---
title: Azure Data Lake Store 目标 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: ebf686807169bb850e5a3ae8fac8cfb0b8ca7791
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061462"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 目标
  “Azure Data Lake Store 目标”  组件允许 SSIS 包将数据写入 Azure Data Lake Store。 支持的文件格式：文本、Avro 和 ORC。 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>配置 Azure Data Lake Store 目标 

1. 将“Azure Data Lake Store 目标”**** 拖放到数据流设计器中，然后双击该组件打开编辑器。  

2.  对于“Azure Data Lake Store 连接管理器”**** 字段，请指定一个现有的 Azure Data Lake Store 连接管理器，或新建一个引用 Azure Data Lake Store 服务的连接管理器。  
  
    1.  对于“文件路径”**** 字段，请指定要将数据写入到的文件名。 如果此文件已存在，则将覆盖其内容。  
  
    2.  对于“文件格式”**** 字段，请指定要使用的文件格式。  
  
        如果文件格式是文本，则必须指定 "**列分隔符字符**" 值。 此外，如果文件中的第一行包含列名称，请选择“在第一个数据行中显示列名称”  。  

        如果文件格式是 ORC，请安装相应平台的 JRE。 
  
3.  指定连接信息后，切换到“列”  页，将源列映射到 SSIS 数据流的目标列。  
