---
title: 任务 6： 验证是否已创建基于域的属性，使用主数据管理器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 042cff6f687bb54466afb2334ad95402de319e94
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207107"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>任务 6：验证通过使用主数据管理器创建了基于域的属性
  在本任务中，将使用“主数据管理器”验证在 **MDS** 中创建了 **State** 实体并且 **Supplier** 实体的 **State** 属性是依赖 **State** 实体的基于域的属性。  
  
1.  切换到“主数据管理器”Web 应用程序。  
  
2.  单击顶部的“SQL Server 2012 Master Data Services”以进入主页。  
  
3.  确保选择了 **Suppliers** 模型，然后单击“资源管理器”。 如果已打开“资源管理器”，则可以刷新该页。  
  
4.  将鼠标悬浮在菜单栏的“实体”上，请注意现在有两个实体：**Supplier** 和 **State**。  
  
     ![实体菜单中使用的状态和供应商](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "实体使用的状态和供应商的菜单")  
  
5.  如果 **State** 实体未打开，则单击该实体。  
  
6.  从列表中选择“GA”。  
  
7.  在右侧的“详细信息”窗格中，将右窗格中的“名称”更改为“Georgia”，然后单击“确定”。  
  
8.  对其他州重复前面的步骤。  
  
    |代码|“属性”|  
    |----------|----------|  
    |CA|California|  
    |CO|Colorado|  
    |IL|Illinois|  
    |DC|District of Columbia|  
    |FL|Florida|  
    |AL|Alabama|  
    |KY|Kentucky|  
    |MA|Massachusetts|  
    |AZ|Arizona|  
    |MI|Michigan|  
    |MN|Minnesota|  
    |NJ|New Jersey|  
    |NV|Nevada|  
    |NY|New York|  
    |OH|Ohio|  
    |确定|Oklahoma|  
    |或|Oregon|  
    |PA|Pennsylvania|  
    |SC|South Carolina|  
    |KS|Kansas|  
    |TN|Tennessee|  
    |TX|Texas|  
    |UT|Utah|  
    |VA|Virginia|  
    |WA|Washington|  
    |WI|Wisconsin|  
    |HI|Hawaii|  
    |MD|Maryland|  
    |CT|Connecticut|  
  
9. 选择任意州条目，然后从工具栏单击“查看事务”。 您应在事务列表中看到与刚刚进行的更新对应的事务。  
  
10. 将鼠标悬浮在“实体”菜单上，然后单击“Supplier”。  
  
11. 现在，请注意可以使用下拉列表在“详细信息”窗格中更改 **State** 字段的值。 还可以看到，在左侧的列表中和“详细信息”窗格中的下拉列表中，首先显示代码，然后显示用大括号括起来的名称。 还可以在“详细信息”窗格中更改任何其他值。  
  
     ![状态具有更新的代码和名称属性](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "状态具有更新的代码和名称属性")  
  
## <a name="next-step"></a>下一步  
 [任务 7：在 Excel 中查看使用主数据管理器所做的更新](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)  
  
  
