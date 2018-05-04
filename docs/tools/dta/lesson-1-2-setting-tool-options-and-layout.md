---
title: 设置工具选项和布局 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b197e970df26c5d48ccaf18603df107f0f3785db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-2---setting-tool-options-and-layout"></a>第 1-2 课 - 设置工具选项和布局
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
您可以设置用于配置数据库引擎优化顾问图形用户界面 (GUI) 在启动时的显示内容、使用的字体以及其他工具功能的选项，从而为您的使用方式提供最佳支持。 通过本页的练习将让您熟悉可设置的各选项及其设置方式。  
  
### <a name="set-the-tool-options"></a>设置工具选项  
  
1.  启动数据库引擎优化顾问。 在 Windows“开始”菜单中，依次指向“所有程序”、[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 和“性能工具”，然后单击“数据库引擎优化顾问”。  
  
2.  在“工具”  菜单上，单击“选项” 。  
  
3.  在“选项”对话框中，查看下列选项：  
  
    -   展开“启动时”列表，查看数据库引擎优化顾问在启动时可显示的内容。 默认情况下，选择“显示新会话”。  
  
    -   单击“更改字体”，查看在“常规”选项卡中可以为数据库和表的列表选择的字体。执行优化后，为此选项选择的字体也将用于数据库引擎优化顾问的建议网格和报表中。 默认情况下，数据库引擎优化顾问使用系统字体。  
  
    -   “最近使用的列表中的项数”可设置为 **1** 到 **10** 之间的数字。 此选项设置在单击“文件”菜单上的“最近使用的会话”或“最近使用的文件”时，列表中可以显示的最大项数。 默认情况下，此选项设置为 **4**。  
  
    -   选中“记住我上次的优化选项”时，默认情况下，数据库引擎优化顾问会将为上一优化会话指定的优化选项用于下一优化会话中。 清除此复选框，以便使用数据库引擎优化顾问优化选项的默认设置。 默认情况下，将选中此选项。  
  
    -   默认情况下，将选中“在永久删除会话之前询问”，避免意外删除优化会话。  
  
    -   默认情况下，将选中“在停止会话分析之前询问”，避免在数据库引擎优化顾问完成工作负载分析之前意外停止优化会话。  
  
## <a name="next-lesson"></a>下一课  
[第 2 课：使用数据库引擎优化顾问](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
