---
title: 服务器元素 (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 23609b4054b456eed8c95659a3984d3f2f03aec3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307876"
---
# <a name="server-element-dta"></a>服务器元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

包含要优化的数据库所驻留的服务器的标识信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 **DTAInput** 元素必须出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 (DTA)](../../tools/dta/dtainput-element-dta.md)|  
|**子元素**|[服务器的名称元素 (DTA)](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [服务器的数据库元素 (DTA)](../../tools/dta/database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>备注  
 只能为 **Server** 元素指定一个 **DTAInput** 元素。 在 DTA XML 架构中，该元素的名称为 **ServerDetailsTypecomplexType** 。 请不要将此 **Server** 元素与 **Configuration** 元素的子元素混淆。 有关详细信息，请参阅[用于配置的服务器元素 (DTA)](../../tools/dta/server-element-for-configuration-dta.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
