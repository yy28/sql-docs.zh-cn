---
title: 推断维度成员（渐变维度向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d76a6f8fc587df4418ee51a8e2a6260b514ee82
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>推断维度成员（渐变维度向导）
  可以使用 **“推断维度成员”** 对话框指定使用推断成员的选项。 当事实数据表引用尚未加载的维度成员时，存在推断成员。 当加载推断成员的数据后，可以更新现有记录，而不必创建一个新记录。  
  
 若要了解有关此向导的详细信息，请参阅 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)。  
  
## <a name="options"></a>“常规”  
 **启用推断成员支持**  
 如果选择启用推断成员，必须选择以下两个选项之一。  
  
 **带更改类型的列均为空**  
 指定是否对新推断成员记录中所有带更改类型的列输入空值。  
  
 **使用布尔值列指示当前记录是否为推断成员**  
 指定是否使用一个现有的布尔值列来指示当前记录是不是推断成员。  
  
 **推断成员指示器**  
 如果如上所述选择了使用布尔值列来指示推断成员，请从该列表中选择此列。  
  
## <a name="see-also"></a>另请参阅  
 [使用渐变维度向导配置输出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
