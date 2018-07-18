---
title: 服务器元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c152b69c2d19be43c833e2f6418225f233e46074
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236037"
---
# <a name="server-element-dta"></a>服务器元素 (DTA)
  包含要优化的数据库所驻留的服务器的标识信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每次需要`DTAInput`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素&#40;DTA&#41;](dtainput-element-dta.md)|  
|**子元素**|[服务器名称元素&#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [服务器的数据库元素&#40;DTA&#41;](database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 您可以指定只有一个`Server`元素`DTAInput`元素。 在 DTA XML 架构中，该元素的名称为 **ServerDetailsTypecomplexType** 。 请勿将此`Server`使用的子元素`Configuration`元素。 有关详细信息，请参阅[用于配置的服务器元素 (DTA)](server-element-for-configuration-dta.md)。  
  
## <a name="example"></a>示例  
 以下示例说明如何在 SERVER001 的 **AdventureWorks** 数据库中指定 **Sales.SalesPerson** 表：  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
