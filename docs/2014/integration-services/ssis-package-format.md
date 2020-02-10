---
title: SSIS 包格式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f59ed0eee86f17fdda568caa5c1a1dc7252c6d9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055348"
---
# <a name="ssis-package-format"></a>SSIS 包格式
  在当前版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中，我们对包格式（.dtsx 文件）进行了重大更改，以方便读取格式和比较包。 您还可以更可靠地合并不包含冲突更改或以二进制格式存储的更改的包。  
  
 若要查看当前的 .dtsx 包文件格式，请参阅[ \[.dtsx\]：数据转换服务包 XML 文件格式规范](https://go.microsoft.com/fwlink/?LinkId=233251)。  
  
 下面的列表概述了这些文件格式更改。 若要查看这些更改的代码示例，请参阅 [SQL Server 2012 中的包格式更改](https://go.microsoft.com/fwlink/?LinkId=233255)。  
  
-   应用了格式约定以将 .dtsx 文件处理为易于读取和理解的形式。  
  
-   格式更为简洁。 每个属性的单独元素始终作为特性（PackageFormatVersion 除外）。 特性将按字母顺序列出，且不再保留具有默认值的属性。 最后，可多次出现的元素现已包含在父元素中。  
  
-   可由其他对象引用的包中的大多数对象现具有在包 XML 中定义的 `refId` 属性。 现在将保留 `refID`，而不是保留沿袭 ID。 沿袭 ID 仍在运行时使用并在加载包时重新生成。  
  
     与 GUID 或整数值相比，`refId` 值是可读且可理解的唯一字符串。 此字符串类似于早期版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中用于包配置的路径值。  
  
     如果要合并两个包版本之间的更改，可在查找/替换操作中使用 `refId` 来确保已正确更新对该对象的所有引用。  
  
-   布局信息已包含在 CData 部分。  
  
-   批注将以明文形式保留。 这样便于提取自动生成的文档的信息。  
  
  
