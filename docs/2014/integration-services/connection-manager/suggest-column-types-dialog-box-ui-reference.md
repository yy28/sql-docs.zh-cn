---
title: “提供列类型建议”对话框 UI 参考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aba9a971b703a3344fc209c1c01943f10c76d767
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833062"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>“提供列类型建议”对话框 UI 参考
  可以使用 **“提供列类型建议”** 对话框，根据文件内容抽样指定平面文件连接管理器中的列的数据类型和长度。  
  
 若要了解有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]使用的数据类型的详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="options"></a>选项  
 **行数**  
 键入或选择算法使用的示例中的行数。  
  
 **建议使用最小整数数据类型**  
 清除此复选框可以略过评估。 选中此复选框之后，将为包含整型数字数据的列确定可能的最小整型数据类型。  
  
 **建议使用最小的实型数据类型**  
 清除此复选框可以略过评估。 选中此复选框之后，将确定包含实型数字数据的列是否可以使用较小的实型数据类型 DT_R4。  
  
 **使用下列值标识布尔值列**  
 键入要用作布尔值 True 和 False 的两个值。 两个值必须用逗号分隔，并且第一个值代表 True。  
  
 **填充字符串列**  
 选中此复选框，可以启用字符串填充。  
  
 **填充百分比**  
 对于字符数据类型的列，键入或选择列长度增加的百分比。 百分比必须为整数。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../integration-services-error-and-message-reference.md)   
 [平面文件连接管理器](file-connection-manager.md)  
  
  
