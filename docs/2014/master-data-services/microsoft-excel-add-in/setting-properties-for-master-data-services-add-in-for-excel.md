---
title: 设置用于 Excel 的 Master Data Services 外接程序的属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 56d3b122b7a458bad7522c766559e1d775b31ef7
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905929"
---
# <a name="setting-properties-for-master-data-services-add-in-for-excel"></a>设置用于 Excel 的 Master Data Services 外接程序的属性
  用于 Excel 的 Master Data Services 外接程序设置确定将 MDS 中的数据加载到 Excel 外接程序的方式和将 Excel 外接程序中的数据发布到 MDS 的方式。  
  
 若要设置 Excel 外接程序，请打开“Excel”，单击“主数据”菜单，然后单击“设置”。 具有对 Excel 的访问权限的任何人都可以更改这些设置。 这些设置适用于打开了 Excel 的计算机。  
  
## <a name="excel-add-in-settings"></a>Excel 外接程序设置  
  
||||  
|-|-|-|  
|选项卡和部分|设置|Description|  
|设置：发布|发布时显示 **“发布并添加批注”** 对话框|如果在单击 **“发布”** 之后选择显示 **“发布并添加批注”** 对话框，您便可以为所有更改输入单个批注或为每个更改输入一个批注。<br /><br /> 取消选择可指定启动发布过程时不显示 **“发布并添加批注”** 对话框。 您将没有机会输入批注。|  
|设置：版本|版本选择|选择将加载到 Excel 外接程序中的主数据的版本。 可以是：<br /><br /> **“无”** 以便不将任何版本设置为默认版本；<br /><br /> **“最早”** 以将默认版本设置为最早版本； **“最新”** 以将默认版本设置为最新版本。|  
|设置：日志记录|打开详细日志记录|为启用日志记录进程的主数据从 MDS 加载到 Excel 外接程序，以便记录在服务中的每个命令的结果。|  
|设置：批大小|要加载的单元格数|选择一个数目，指示从 MDS 服务器加载到 Excel 的一个批次中将加载几千个单元格。 默认值为 50,000 个单元格。|  
|设置：批大小|要发布的单元格数|选择一个数目，指示从 Excel 返回到服务器的一个批次中将发布几千个单元格。 默认值为 50,000 个单元格。|  
|设置：添加到安全列表的服务器|全部清除|单击可清除在打开关联的快捷查询文件时被指定为安全的连接列表。|  
|数据：筛选器|显示针对大型数据集的筛选警告|如果要从 MDS 中加载到 Excel 的数据集超过最大行数或列数，则单击此选项会显示警告。|  
|数据：筛选器|最大行数|选择要加载的行数的阈值，超过该值将发布一个筛选器警告。|  
|数据：筛选器|最大列数|选择要加载的列数的阈值，超过该值将发布一个筛选器警告。|  
|数据：单元格格式|属性值更改时更改颜色|单击此选项可以指定：当您使用 MDS 库中的新数据刷新 Excel 外接程序表时，如果某个单元格中的属性值发生更改，则更改该单元格的颜色。|  
|数据：单元格格式|添加成员时更改颜色|单击此选项可以指定：当您使用 MDS 库中的新数据刷新 Excel 外接程序表时，如果在某个行中添加了新成员，则更改该行的单元格的颜色。|  
  
  
