---
title: "HDFS 文件源 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b7ed3c3789b7c28476719422f600106a73bfebd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="hdfs-file-source"></a>HDFS 文件源
  “HDFS 文件源”组件允许 SSIS 包从 HDFS 文件中读取数据。 支持的文件格式有文本和 Avro。 （不支持 ORC 源。）  
  
 若要配置“HDFS 文件源”，请将“HDFS 文件源”拖放到数据流设计器中，然后双击该组件打开编辑器。  
  
 ![HDFS 文件源编辑器](../../integration-services/data-flow/media/hdfs-file-source.png "HDFS 文件源编辑器")  
  
## <a name="options"></a>选项  
 在“Hadoop 文件源编辑器”  对话框的“常规”  选项卡上配置以下选项。  
  
|字段|Description|  
|-----------|-----------------|  
|**Hadoop 连接**|指定一个现有的 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 HDFS 文件的托管位置。|  
|**文件路径**|指定 HDFS 文件的文件名。|  
|**文件格式**|指定 HDFS 文件的格式。 可用选项为文本和 Avro。 （不支持 ORC 源。）|  
|**列分隔符字符**|如果你选择文本格式，请指定列分隔符字符。|  
|**第一个数据行中的列名称**|如果你选择文本格式，请指定文件中的第一行是否包含列名称。|  
  
 配置这些选项后，选择“列”  选项卡，将源列映射到数据流中的目标列。  
  
## <a name="see-also"></a>另請參閱  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 文件目标](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
