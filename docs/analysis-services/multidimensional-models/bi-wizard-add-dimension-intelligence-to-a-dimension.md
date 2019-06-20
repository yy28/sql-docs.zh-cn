---
title: 向维度添加维度智能 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad714bfefa8010664a8105eebf1f45d63799847c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62717334"
---
# <a name="bi-wizard---add-dimension-intelligence-to-a-dimension"></a>BI 向导 - 向维度中添加维度智能
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以在多维数据集或维度中添加维度智能增强功能，以便为维度指定标准业务类型。 此增强功能还将为维度属性指定相应的类型。 客户端应用程序在分析数据时可以使用这些指定的类型。  
  
 若要添加维度智能，请使用商业智能向导，并在 **“选择增强功能”** 页中选择 **“定义维度智能”** 选项。 然后，此向导将引导您完成相应的步骤，以选择要应用维度智能的维度，并标识所选维度的属性。  
  
## <a name="selecting-a-dimension"></a>选择维度  
 在向导的第一个 **“设置维度智能选项”** 页中，指定要应用维度智能的维度。 添加到此所选维度中的维度智能增强功能将使维度发生更改。 所有包含选定维度的多维数据集都将继承这些更改。  
  
> [!NOTE]  
>  如果选择 **“帐户”** 作为维度，则要指定维度的帐户智能。 有关详细信息，请参阅 [向维度中添加帐户智能](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="specifying-dimension-attributes"></a>指定维度属性  
 在 **“定义维度智能”** 页的 **“维度类型”** 列表中，所做选择将设置维度的 **Type** 属性。 **Type** 属性设置可以为服务器和客户端应用程序提供有关维度内容的信息。 某些设置只为客户端应用程序提供指导；这些设置是可选的。 其他设置（如“帐户”或“时间”）则确定特定的行为，它们在实现特定商业智能增强功能时可能是必需的。 例如，SQL Server Management Studio 使用维度类型标识“货币”维度，并设置合适的货币换算规则。 **“维度类型”** 的默认设置是 **“常规”**，该设置不对维度内容进行任何假设。  
  
 选择维度类型后，请在 **“维度属性”** 的 **“包含”** 列中，选中在维度中有其相应属性的每个标准属性类型旁边的复选框。 最后，在“维度属性”列中展开下拉列表，并在维度中选择对应于所选属性类型的属性。 如果从该列表选择特性，将会设置特性的 **Type** 属性。  
  
 例如，您希望向“帐户”维度添加维度智能。 在 **“维度类型”** 中，选择 **“帐户”**。 然后，如果维度有 **“帐户类型”** 和 **“帐户说明”** 属性，则在 **“包含”** 列中选中 **“帐户名”** 和 **“帐户类型”** 帐户类型的复选框。 接着，在 **“维度属性”** 列中，将这些帐户类型分别与 **“帐户说明”** 和 **“帐户类型”** 属性关联。  
  
## <a name="see-also"></a>请参阅  
 [使用商业智能向导定义时间智能计算](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  
