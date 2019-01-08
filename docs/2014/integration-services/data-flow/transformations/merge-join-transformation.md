---
title: 合并联接转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e1a581536bb4f2a07dbbdf3d6ca187ac4a6f5250
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767179"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation
  合并联接转换提供了一个输出，该输出是通过使用 FULL、LEFT 或 INNER 联接将两个已排序数据集进行联接而生成的。 例如，可使用 LEFT 联接来联接包含产品信息的表与列出产品的制造国家/地区的表。 结果是一个列出所有产品及其产地国家/地区的表。  
  
 可以按照下列方法来配置合并联接转换：  
  
-   指定联接是 FULL、LEFT 联接，还是 INNER 联接。  
  
-   指定联接所使用的列。  
  
-   指定转换是否将空值处理为等于其他空值。  
  
    > [!NOTE]  
    >  如果不将空值处理为相等的值，则转换将如同 SQL Server 数据库引擎那样处理空值。  
  
 此转换有两个输入和一个输出。 它不支持错误输出。  
  
## <a name="input-requirements"></a>输入要求  
 合并联接转换要求输入已排序的数据。 有关此重要要求的详细信息，请参阅 [为合并转换和合并联接转换排序数据](sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
## <a name="join-requirements"></a>联接要求  
 合并联接转换要求被联接的列具有匹配的元数据。 例如，不能将具有数值数据类型的列和具有字符数据类型的列相联接。 如果数据为字符串数据类型，第二个输入中列的长度必须小于或等于被合并的第一个输入中列的长度。  
  
## <a name="buffer-throttling"></a>缓冲区中止  
 您不再必须配置 `MaxBuffersPerInput` 属性的值，因为 Microsoft 已进行了更改，减少了合并联接转换将占用过多内存的风险。 在合并联接的多个输入以不相等速率生成数据时，有时候可能会发生此问题。  
  
## <a name="related-tasks"></a>Related Tasks  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关如何设置此转换的属性的信息，请单击下列主题之一：  
  
-   [使用合并联接转换扩展数据集](merge-join-transformation.md)  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>请参阅  
 [合并联接转换编辑器](../../merge-join-transformation-editor.md)   
 [合并转换](merge-transformation.md)   
 [Union All 转换](union-all-transformation.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
