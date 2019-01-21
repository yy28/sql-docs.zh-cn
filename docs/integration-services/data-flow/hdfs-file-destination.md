---
title: HDFS 文件目标 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f18f6b0516ab9ae417251e49f5a3cf24fd2aa997
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185003"
---
# <a name="hdfs-file-destination"></a>HDFS 文件目标
  “HDFS 文件目标”组件允许 SSIS 包将数据写入 HDFS 文件。 支持的文件格式：文本、Avro 和 ORC。  
  
 若要配置“HDFS 文件目标”，请将“HDFS 文件源”拖放到数据流设计器中，然后双击该组件打开编辑器。  
  
 ![HDFS 文件目标编辑器](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS File Destination Editor")  
  
## <a name="options"></a>选项  
 在“Hadoop 文件目标编辑器”  对话框的“常规”  选项卡上配置以下选项。  
  
|字段|描述|  
|-----------|-----------------|  
|**Hadoop 连接**|指定现有的一个 Hadoop 连接管理器，或新建一个 Hadoop 连接管理器。 此连接管理器指明 HDFS 文件的托管位置。|  
|**文件路径**|指定 HDFS 文件的文件名。|  
|**文件格式**|指定 HDFS 文件的格式。 可用选项包括“文本”、“Avro”和“ORC”。|  
|**列分隔符字符**|如果你选择文本格式，请指定列分隔符字符。|  
|**第一个数据行中的列名称**|如果你选择文本格式，请指定文件中的第一行是否包含列名称。|  
  
 配置这些选项后，选择“列”  选项卡，将源列映射到数据流中的目标列。  

::: moniker range=">= sql-server-ver15"
## <a name="prerequisite-for-orc-format"></a>ORC 格式的先决条件

使用 ORC 文件格式之前，需要为相应的平台安装 Java 运行时环境 (JRE) 1.7.51 或更高版本。

支持 Zulu 和 Oracle JRE。
-   [Zulu JRE](https://www.azul.com/downloads/zulu/zulu-windows/)
-   [Oracle JRE](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)

### <a name="set-up-the-zulu-jre"></a>设置 Zulu JRE

1. 下载并提取 Zulu OpenJDK 安装 zip 包。

2.  从命令提示符处，运行 `sysdm.cpl`。

3. 在“高级”选项卡上，选择“环境变量”。

4. 在“系统变量”部分中，选择“新建”。

5. 输入变量名称 `JAVA_HOME`。

6. 选择“浏览目录”，导航到 Zulu OpenJDK 的安装文件夹，然后选择 `jre` 子文件夹。 然后选择“确定”。 变量的值将自动进行填充。

7. 选择“确定”，关闭“新建系统变量”对话框。

8. 选择“确定”，关闭“环境变量”对话框。

### <a name="set-up-the-oracle-jre"></a>设置 Oracle JRE

1. 下载并运行 Oracle JRE exe 安装程序。

1. 按照安装程序说明完成安装。

::: moniker-end

## <a name="see-also"></a>另请参阅  
 [Hadoop 连接管理器](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 文件源](../../integration-services/data-flow/hdfs-file-source.md)  
