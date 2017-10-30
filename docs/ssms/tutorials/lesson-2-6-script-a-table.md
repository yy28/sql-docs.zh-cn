---
title: "编写表脚本 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 422a81da1656b9b5c72fdcf1e71979ff0c8c058f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="lesson-2-6---script-a-table"></a>课程 2-6 - 编写表脚本
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以创建脚本，用于选择、插入、更新和删除表，以及用于创建、更改、删除或执行存储过程。  
  
有时您可能需要使用具有多个选项的脚本，如删除一个过程后再创建一个过程，或者创建一个表后再更改一个表。 若要创建组合的脚本，请将第一个脚本保存到“查询编辑器”窗口中，并将第二个脚本保存到剪贴板上，这样就可以在窗口中将第二个脚本粘贴到第一个脚本之后。  
  
 
1.  在“对象资源管理器”中，依次展开服务器、“数据库”、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]、“表”，再右键单击“HumanResources.Employee”，然后指向“编写表脚本为”。  
  
2.  快捷菜单有七个可用脚本选项：“CREATE To”、“DROP To”、“DROP and CREATE To”、“SELECT To”、“INSERT To”、“UPDATE To”和“DELETE To”。 指向“UPDATE To”，再单击“新查询编辑器窗口”。  
  
3.  系统将打开一个新查询编辑器窗口，执行连接并显示完整的更新语句。  
  
    本练习阐释了除编写脚本创建表或存储过程外，脚本编写功能如何实现其他功能。 使用这项新功能可以将数据操作脚本快速添加到项目中，并可轻松编写执行存储过程的脚本。 这可以大量节省多字段的表和过程的执行时间。  
  
 
  
  
  

