---
title: Excel Services 不支持以下功能并且可能无法显示或者只能部分显示以下功能：注释、 形状或其他对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16269f5c0d7b3d64c9639862995dee44146efb9e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743929"
---
# <a name="the-following-features-are-not-supported-by-excel-services-and-may-not-display-or-may-display-only-partially-comments-shapes-or-other-objects"></a>Excel Services 不支持以下功能并且可能无法显示或者只能部分显示以下功能：注释、形状或其他对象
  在您将切片器从 PowerPivot 字段列表添加到 PowerPivot 工作簿时会发生此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用对象|PowerPivot for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Web Access 无法呈现用于控制从 PowerPivot 字段列表添加到某一工作簿的切片器的位置和格式的形状对象。|  
|消息正文|Excel Services 不支持以下功能并且可能无法显示或者只能部分显示以下功能：<br /><br /> 注释、形状或其他对象<br /><br /> 某些功能（例如外部数据查询）显示只能在 Microsoft Excel 中刷新的缓存数据。|  
  
## <a name="explanation"></a>解释  
 Excel Web Access 将显示此错误时在浏览器中打开 PowerPivot 工作簿并单击**详细信息**消息框按钮**不受支持的功能： 此工作簿可能无法按预期显示**。  
  
 出现此错误的原因是因为 PowerPivot 工作簿包含其布局由 Excel 中隐藏的形状对象控制的切片器。 该形状对象在水平和垂直位置上控制切片器的格式和位置。  
  
 Excel Services 无法呈现形状对象，但因为该对象是隐藏的，所以尽管无法呈现，但这并不是问题。  
  
## <a name="user-action"></a>用户操作  
 可以忽略此错误。 单击 **“确定”** 以便关闭该错误消息并且可以放心地继续使用工作簿和切片器。  
  
  
