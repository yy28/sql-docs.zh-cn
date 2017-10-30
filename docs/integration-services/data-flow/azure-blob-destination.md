---
title: "Azure Blob 目标 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobdest.f1
- sql14.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 152d92859c2f4ce96d0cc1ba9b02ffb412d18fde
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-destination"></a>Azure blob 目标
 “Azure blob 目标”  组件允许 SSIS 包将数据写入 Azure blob。 支持的文件格式：CSV 和 AVRO。 
   
 将“Azure blob 目标”拖放到数据流设计器中，然后双击该组件打开编辑器。  
  
 **Azure Blob 目标**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。  
  
1.  对于“Azure 存储空间连接管理器”  字段，请指定一个现有的 Azure 存储空间连接管理器，或新建一个引用 Azure 存储空间帐户的连接管理器。  
  
2.  对于“blob 容器名称”  字段，请指定包含源文件的 blob 容器的名称。  
  
3.  对于“blob 名称”  字段，请指定 blob 的路径。  
  
4.  对于“blob 文件格式”  字段，请指定要使用的 blob 格式。  
  
5.  如果文件格式是 CSV，你必须指定“列分隔符字符”  值。 此外，如果文件中的第一行包含列名称，请选择“在第一个数据行中显示列名称”  。  
  
6.  指定连接信息后，切换到“列”  页，将源列映射到 SSIS 数据流的目标列。  
  
  

