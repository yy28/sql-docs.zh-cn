---
title: "服务器属性（“杂项服务器设置”页）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.serverproperties.miscserversettings.f1
ms.assetid: b170c066-30cd-42dd-8d34-aa129ea09551
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 53069a083eff6c49fa5198743eb626ca429b96d1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="server-properties---misc-server-settings-page"></a>服务器属性 -“杂项服务器设置”页
  使用此页可以查看或修改服务器设置。  
  
## <a name="options"></a>选项  
 **用户的默认语言**  
 指定所有新建登录名的默认语言。  
  
 **允许触发器激发其他触发器**  
 控制触发器是否可以执行启动另一个触发器的操作。 清除此选项后，触发器不能由另外一个触发器来激发。 选中此选项时，触发器可以由其他触发器来激发，级联等级最高为 32 级。  
  
 **使用查询调控器防止查询长时间运行**  
 指定查询运行时间的上限。 查询开销是指在特定硬件配置中执行查询所需的估计占用时间（秒）。 查询调控器默认为关闭，允许运行所有查询。 如果选中此选项，则必须在下面的文本框中输入时间限制。 如果为该选项指定一个非零、非负的数值，则查询调控器将不允许执行估计开销超过该值的查询。  
  
 **将两位数的年份解释为介于**  
 指定 100 年的日期范围，用于解释针两位数年份值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将两位数日期值解释为指定范围内以这两位数值结尾的年份。  
  
 在右侧的框中设置结束年份。 保存结束年份时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会自动在左侧的框中填充起始年份。  
  
 **配置值**  
 显示此窗格上选项的配置值。 如果更改了这些值，请单击 **“运行值”** 以查看更改是否已生效。 如果更改未生效，则必须首先重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 **“运行值”**  
 查看此窗格上选项的当前运行值。 这些值是只读的。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
