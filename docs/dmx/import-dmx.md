---
description: IMPORT (DMX)
title: 导入 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5da00163792b18bfd62ed0db4be0945f358115e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352683"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  将挖掘模型或挖掘结构从 Analysis Services 备份文件 (.abf) 文件加载到服务器中。  
  
## <a name="syntax"></a>语法  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>参数  
 *filename*  
 一个包含要导入的文件的名称和位置的字符串。  
  
## <a name="remarks"></a>备注  
 如果未指定对象，则系统将加载 .dmb 文件的所有内容。 如果 .dmb 文件包含服务器中不存在的数据库，则系统将创建该数据库。  
  
 只有数据库或服务器管理员才能导出或导入对象。  
  
## <a name="import-from-file-example"></a>从文件示例导入  
 下面的示例将包含关联模型和结构的文件的所有内容全部导入到当前服务器中。  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [导出 &#40;DMX&#41;](../dmx/export-dmx.md)   
 [导出和导入数据挖掘对象](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
