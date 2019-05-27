---
title: 编辑表属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f629b0f7905cce4547d76ddfe97adc7dedd17079
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728855"
---
# <a name="edit-the-table-properties"></a>编辑表属性

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用此对话框可编辑所选表中要捕获更改的特定列。 您还可以编辑 **“安全角色”** 和 **“捕获实例”** 信息。  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>编辑要在 CDC 实例中包含的列  
  
1.  执行下列一种或两种操作：  
  
    -   选中要包括的任何其他列旁边的复选框。  
  
    -   取消选中不想再包括的任何列旁边的复选框。  
  
### <a name="to-edit-the-security-role"></a>编辑安全角色  
  
1.  键入一个新名称或在 **“安全角色”** 字段中编辑安全角色的名称。  
  
### <a name="to-create-a-new-capture-instance"></a>创建新的捕获实例  
  
1.  在 **“安全角色”** 部分的 **“名称”** 字段中，输入捕获实例的名称。 默认情况下，在该字段中输入的名称是当前捕获实例的名称加上在该名称末尾添加的 **_NEW** （例如 **old_instance_NEW**）。  
  
2.  将捕获实例保存为以下项之一：  
  
    -   **新建捕获实例**：在此情况下，将保存新的捕获实例并且不删除旧的捕获实例。  
  
         **注意**：每个表不能具有超过两个捕获实例。 如果已有两个捕获实例，则此选项不可用。  
  
    -   **替换现有捕获实例**：在此情况下，将删除当前捕获实例并用你创建的捕获实例替换。 如果为此表定义了两个捕获实例，则您必须选择要替换的一个实例。  
  
 **注意**：可以从“表”选项卡的表列表中删除某一捕获实例。  
  
 在此对话框中输入完信息后，单击 **“确定”** 以接受更改。  
  
## <a name="see-also"></a>另请参阅  
 [如何编辑 CDC 实例属性](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [对为捕获更改选择的表进行更改](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
