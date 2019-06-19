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
manager: jroth
ms.openlocfilehash: 5c7e6aab3e3b33d02adcb067fff46b49973191b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698232"
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
