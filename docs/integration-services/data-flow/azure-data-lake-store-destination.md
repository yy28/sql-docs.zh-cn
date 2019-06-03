---
title: Azure Data Lake Store 目标 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d934cafef262f5c07b5eeac95d65abd776d8bb35
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403040"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 目标

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  “Azure Data Lake Store 目标”  组件允许 SSIS 包将数据写入 Azure Data Lake Store。 支持的文件格式为：文本、Avro 和 ORC。 
  
 “Azure Data Lake Store 目标”  是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)组件。
 
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

## <a name="prerequisite-for-orc-file-format"></a>ORC 文件格式的先决条件
使用 ORC 文件格式时需要 Java。
Java 版本的体系结构（32/64 位）应与要使用的 SSIS 运行时的体系结构一致。
已测试以下 Java 版本。

- [Zulu OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE 运行时环境 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>安装 Zulu OpenJDK
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

### <a name="set-up-oracles-java-se-runtime-environment"></a>安装 Oracle Java SE 运行时环境
1. 下载并运行 exe 安装程序。
2. 按照安装程序说明完成安装。