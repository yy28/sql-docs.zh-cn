---
title: Azure blob 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobsrc.f1
- sql11.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0f1e39088c96239caae8e757407d3338733fcb76
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916655"
---
# <a name="azure-blob-source"></a>Azure blob 源
 借助“Azure blob 源”  组件，SSIS 包可以读取 Azure blob 中的数据。 支持的文件格式：CSV 和 AVRO。 若要查看 Azure blob 源的编辑器，请将“Azure blob 源”  拖放到数据流设计器上，然后双击它打开编辑器。  
  
1.  对于“Azure 存储空间连接管理器” **** 字段，请指定一个现有的 Azure 存储空间连接管理器，或新建一个引用 Azure 存储空间帐户的连接管理器。  
  
2.  对于“blob 容器名称” **** 字段，请指定包含源文件的 blob 容器的名称。  
  
3.  对于“blob 名称” **** 字段，请指定 blob 的路径。  
  
4.  对于“blob 文件格式” **** 字段，请指定要使用的 blob 格式。  
  
5.  如果文件格式是 CSV，你必须指定“列分隔符字符” **** 值。 此外，如果文件中的第一行包含列名称，请选择“在第一个数据行中显示列名称” **** 。  
  
6.  指定连接信息后，切换到“列” **** 页，将源列映射到 SSIS 数据流的目标列。  
  
  
