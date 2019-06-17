---
title: 原始文件源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1bedefd277f1be7f44d807e6539097dd24f5ab2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900907"
---
# <a name="raw-file-source"></a>原始文件源
  原始文件源从文件中读取原始数据。 因为数据的表示方式是源所固有的，所以数据无需转换，并且几乎不需要分析。 这意味着原始文件源可以比其他源（如平面文件和 OLE DB 源）更快地读取数据。  
  
 原始文件源用于检索先前由原始文件目标写入的原始数据。 您还可以将原始文件源指向一个仅包含列的空原始文件（仅元数据文件）。 使用原始文件目标生成仅元数据文件而无需运行包。 有关详细信息，请参阅 [Raw File Destination](raw-file-destination.md)。  
  
 原始文件格式包含排序信息。 原始文件目标将保存所有排序信息，包括字符串列的比较标志。 原始文件源读取和采用排序信息。 您可以使用高级编辑器选择将原始文件源配置为忽略文件中的排序标志。 有关比较标志的详细信息，请参阅 [Comparing String Data](comparing-string-data.md)。  
  
 可以通过指定原始文件源所读取的文件的名称来配置原始文件。  
  
> [!NOTE]  
>  此源不使用连接管理器。  
  
 此源具有一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-raw-file-source"></a>原始文件源的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [原始文件自定义属性](raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置该组件属性的信息，请参阅 [设置数据流组件属性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相关内容  
  
-   sqlservercentral.com 上的博客文章： [原始文件令人生畏](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx)。  
  
## <a name="see-also"></a>请参阅  
 [Raw File Destination](raw-file-destination.md)   
 [数据流](data-flow.md)  
  
  
