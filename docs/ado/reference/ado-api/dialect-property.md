---
title: Dialect 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef18eb3d6251bc07ae25ef8cbc3445a87b8390b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810515"
---
# <a name="dialect-property"></a>Dialect 属性
指示的方言[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性。 方言定义的语法和提供程序使用来分析该字符串或流的一般规则。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 **方言**属性包含有效的 GUID 表示的命令文本或流的方言。 此属性的默认值是 {C8B521FB-5CF3-11CE-ADE5-00AA0044773D} 指示提供程序应选择如何解释命令文本或流。  
  
## <a name="remarks"></a>备注  
 当用户读取此属性影响; 的值时，ADO 将不会查询提供程序它将返回当前存储中的值的字符串表示形式[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
 当用户设置**方言**属性，ADO 验证 GUID，并引发错误，如果提供的值不是有效的 GUID。 请参阅您的提供商来确定支持的 GUID 值的文档**方言**属性。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Execute 方法（ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)
