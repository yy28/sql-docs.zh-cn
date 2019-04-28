---
title: 选项 （文本编辑器-XML-格式页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 0c792bc2b37bbaae5161b856a7423adb4b707228
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843811"
---
# <a name="options-text-editor---xml---formatting-page"></a>选项（“文本编辑器”-“XML”-“格式”页）

使用此对话框，可以为 XML 编辑器指定格式设置。 可从“工具”菜单访问“选项”对话框。  
  
> [!NOTE]  
> 从“选项”对话框依次选择“文本编辑器”文件夹、“XML”文件夹和“格式”选项后，这些设置将可用。  
  
## <a name="attributes"></a>特性  
 **保留手动属性格式化**  
 请不要重新设置属性的格式。 这是默认设置。  
  
> [!NOTE]  
>  如果这些属性位于多行上，则编辑器会缩进属性的每一行，以与父元素的缩进大小相匹配。  
  
 **使属性每个单独的行上对齐**  
 垂直对齐第二个属性和后续属性，以便与第一个属性的缩进大小相匹配。 下面的 XML 文本就是如何对齐属性的示例：  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>自动重新设置格式  
 **在从剪贴板粘贴时。**  
 重新设置从剪贴板粘贴的 XML 文本的格式。  
  
 **在完成结束标记**  
 在完成结束标记时重新设置元素的格式。  
  
## <a name="mixed-content"></a>混合内容  
 **默认情况下为格式混合的内容。**  
 尝试重新设置混合内容的格式，在 `xml:space="preserve"` 作用域中找到该内容时除外。 这是默认设置。  
  
 如果某个元素同时包含文本和标记，则这些内容会被视为混合内容。 下面是包含混合内容的元素的示例：  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</dir>  
  
## <a name="see-also"></a>请参阅  
 [XML 编辑器 (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md)  
