---
title: 推断维度成员（渐变维度向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1f6b53ffd05c7076a849b954f478757c12405e34
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804860"
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>推断维度成员（渐变维度向导）
  可以使用 **“推断维度成员”** 对话框指定使用推断成员的选项。 当事实数据表引用尚未加载的维度成员时，存在推断成员。 当加载推断成员的数据后，可以更新现有记录，而不必创建一个新记录。  
  
 若要了解有关此向导的详细信息，请参阅 [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)。  
  
## <a name="options"></a>选项  
 **启用推断成员支持**  
 如果选择启用推断成员，必须选择以下两个选项之一。  
  
 **带更改类型的列均为空**  
 指定是否对新推断成员记录中所有带更改类型的列输入空值。  
  
 **使用布尔值列指示当前记录是否为推断成员**  
 指定是否使用一个现有的布尔值列来指示当前记录是不是推断成员。  
  
 **推断成员指示器**  
 如果如上所述选择了使用布尔值列来指示推断成员，请从该列表中选择此列。  
  
## <a name="see-also"></a>请参阅  
 [使用渐变维度向导配置输出](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
