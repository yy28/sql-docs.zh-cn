---
title: Union All 转换编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- Union All Transformation Editor
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b62fb5e33311f1011911c40fc858723b218bac55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054831"
---
# <a name="union-all-transformation-editor"></a>Union All 转换编辑器
  可以使用 **“Union All 转换编辑器”** 对话框，将多个输入行集合并到单个输出行集中。 通过在数据流中包含 Union All 转换，可以从多个数据流合并数据、通过嵌套 Union All 转换来创建复杂数据集、以及在更正数据中的错误之后重新合并行。  
  
 若要了解有关 Union All 转换的详细信息，请参阅 [Union All Transformation](data-flow/transformations/union-all-transformation.md)。  
  
## <a name="options"></a>选项  
 **输出列的名称**  
 为每一列键入一个别名。 默认值为第一个（引用）输入中输入列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 **Union All 输入 1**  
 从第一个（引用）输入中可用输入列的列表中选择。 映射的列的元数据必须匹配。  
  
 **Union All 输入 n**  
 从第二个或其他输入中可用输入列的列表中选择。 映射的列的元数据必须匹配。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用 Union All 转换来合并数据](data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [合并转换](data-flow/transformations/merge-transformation.md)   
 [合并联接转换](data-flow/transformations/merge-join-transformation.md)  
  
  
