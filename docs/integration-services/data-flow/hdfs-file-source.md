---
title: HDFS 文件源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4f3866b56645b9e484f07ac775f4b642defc5d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="hdfs-file-source"></a>HDFS 文件源
  “HDFS 文件源”组件允许 SSIS 包从 HDFS 文件中读取数据。 支持的文件格式有文本和 Avro。 （不支持 ORC 源。）  
  
 若要配置“HDFS 文件源”，请将“HDFS 文件源”拖放到数据流设计器中，然后双击该组件打开编辑器。  
  
 ![HDFS 文件源编辑器](../../integration-services/data-flow/media/hdfs-file-source.png "HDFS File Source Editor")  
  
## <a name="options"></a>“常规”  
 在“Hadoop 文件源编辑器”  对话框的“常规”  选项卡上配置以下选项。  
  
|字段|Description|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 HDFS 文件的托管位置。|  
|**文件路径**|指定 HDFS 文件的文件名。|  
|**文件格式**|指定 HDFS 文件的格式。 可用选项为文本和 Avro。 （不支持 ORC 源。）|  
|**列分隔符字符**|如果你选择文本格式，请指定列分隔符字符。|  
|**第一个数据行中的列名称**|如果你选择文本格式，请指定文件中的第一行是否包含列名称。|  
  
 配置这些选项后，选择“列”  选项卡，将源列映射到数据流中的目标列。  
  
## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 文件目标](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
