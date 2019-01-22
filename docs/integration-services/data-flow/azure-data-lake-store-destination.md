---
title: Azure Data Lake Store 目标 | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0bfa4975840a93f0081cdc7fed376c748416fa06
ms.sourcegitcommit: e2fa721b6f46c18f1825dd1b0d56c0a6da1b2be1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54211028"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 目标
  “Azure Data Lake Store 目标”  组件允许 SSIS 包将数据写入 Azure Data Lake Store。 支持的文件格式为：文本、Avro 和 ORC。 
  
 “Azure Data Lake Store 目标”是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)组件。
 
> [!NOTE]
> 若要确保 Azure Data Lake Store 连接管理器和使用它的组件（即 Azure Data Lake Store 源和 Azure Data Lake Store 目标）可连接到服务，请确保在 [此处](https://www.microsoft.com/download/details.aspx?id=49492)下载最新版本的 Azure 功能包。 

## <a name="configure-the-azure-data-lake-store-destination"></a>配置 Azure Data Lake Store 目标  
1. 将“Azure Data Lake Store 目标”  拖放到数据流设计器中，然后双击该组件打开编辑器。  

2.  对于“Azure Data Lake Store 连接管理器”  字段，请指定一个现有的 Azure Data Lake Store 连接管理器，或新建一个引用 Azure Data Lake Store 服务的连接管理器。  
  
    1.  对于“文件路径”  字段，请指定要将数据写入到的文件名。 如果此文件已存在，则将覆盖其内容。  
  
    2.  对于“文件格式”  字段，请指定要使用的文件格式。  
  
       如果文件格式是文本，则必须指定“列分隔符字符”  值。 此外，如果文件中的第一行包含列名称，请选择“在第一个数据行中显示列名称”  。  

       如果文件格式是 ORC，则需要安装相应平台的 Java Runtime Environment (JRE)。
  
3.  指定连接信息后，切换到“列”  页，将源列映射到 SSIS 数据流的目标列。  
