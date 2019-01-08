---
title: 连接已注册的服务器和对象资源管理器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: d6b3911f-68b4-4483-831b-df89d6400add
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 374d75c18adc091eaf6a01ae1164a529a34accee
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521308"
---
# <a name="connect-with-registered-servers-and-object-explorer"></a>与已注册的服务器和对象资源管理器连接
  本教程演示如何使用已注册的服务器和对象资源管理器。  
  
 本教程使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。 为了帮助增强安全性，默认情况下不会安装示例数据库。 有关详细信息，请参阅 [安装 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com)。  
  
## <a name="connecting-to-servers"></a>连接到服务器  
 已注册的服务器组件的工具栏包含用于 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的按钮。 可以注册上述的一个或多个服务器类型以便于管理。 请尝试以下练习来注册 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
#### <a name="to-register-the-database"></a>注册数据库  
  
1.  在“已注册的服务器”工具栏中，如有必要，请单击“数据库引擎”。 （该选项可能已选中。）  
  
2.  展开“数据库引擎”。  
  
3.  右键单击“本地服务器组”，然后单击“新建服务器注册”。  
  
4.  在“新建服务器注册”对话框中的“服务器名称”文本框中，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。  
  
5.  在“已注册的服务器名称”框中，键入 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
6.  上**连接属性**选项卡上，在**连接到数据库**列表中，选择**\<浏览服务器...> >**。  
  
7.  在“查找数据库”对话框中，单击“是”。  
  
8.  在“查找服务器上的数据库”对话框中，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然后单击“确定”。  
  
9. 要验证服务器已正确注册，请单击“测试”。  
  
10. 在“新建服务器注册”对话框中，单击“保存”。  
  
## <a name="connecting-with-object-explorer"></a>与对象资源管理器连接  
 与已注册的服务器类似，对象资源管理器也可以连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
#### <a name="to-connect-with-object-explorer"></a>与对象资源管理器连接  
  
1.  在对象资源管理器的工具栏中，单击“连接”显示可用连接类型列表，再选择“数据库引擎”。  
  
2.  在“连接到服务器”对话框中的“服务器名称”文本框中，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。  
  
3.  单击“选项”，然后浏览各选项。  
  
4.  若要连接到服务器，请单击“连接”。 如果已经连接，则此操作会使您直接返回到对象资源管理器，并将该服务器设置为焦点。  
  
     利用对象资源管理器，可以管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理、复制和数据库邮件。 对象资源管理器只能管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssIS](../../includes/ssis-md.md)]的部分功能。 上述每个组件都有其他专用工具。  
  
5.  在对象资源管理器中，展开“数据库”文件夹并且选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
     请注意，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将系统数据库放在一个单独的文件夹中。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [更改环境布局](lesson-1-3-change-the-environment-layout.md)  
  
  
