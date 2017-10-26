---
title: "导入 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5510631430ed75a04dd9685d1197f60c64a85aa8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将挖掘模型或挖掘结构从 Analysis Services 备份文件 (.abf) 文件加载到服务器中。  
  
## <a name="syntax"></a>语法  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>参数  
 *文件名*  
 一个包含要导入的文件的名称和位置的字符串。  
  
## <a name="remarks"></a>注释  
 如果未指定对象，则系统将加载 .dmb 文件的所有内容。 如果 .dmb 文件包含服务器中不存在的数据库，则系统将创建该数据库。  
  
 只有数据库或服务器管理员才能导出或导入对象。  
  
## <a name="import-from-file-example"></a>从文件示例导入  
 下面的示例将包含关联模型和结构的文件的所有内容全部导入到当前服务器中。  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [导出 &#40; DMX &#41;](../dmx/export-dmx.md)   
 [导出和导入数据挖掘对象](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

