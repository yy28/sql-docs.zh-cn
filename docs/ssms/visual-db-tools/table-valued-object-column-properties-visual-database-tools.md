---
title: 表值对象（列）属性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81ab7f8547376344a1106a473f6f5ef69a3b1b9f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792975"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>表值对象（列）属性 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在查询设计器和视图设计器的“关系图”窗格中选择表值对象中的列时，将显示这些属性。  
  
> [!NOTE]  
> 本主题中的属性按类别排序，而不是按字母顺序排序。  
  
> [!NOTE]  
> 根据当前设置或版本的不同，所看到的对话框和菜单命令可能与帮助中描述的对话框和菜单命令有所不同。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。  
  
**标识类别**  
展开此项可显示“名称”属性。  
  
**名称**  
显示所选列的名称。  
  
**查询设计器类别**  
展开此项可显示“允许 Null 值”、“排序规则”、“数据类型”、“长度”、“精度”、“确定位数”和“大小”属性。  
  
**允许 Null 值**  
显示列的数据类型是否允许空值。  
  
**排序规则**  
显示所选列的排序规则设置。 排序规则可以在表设计器的“列属性”选项卡中进行设置。  
  
**数据类型**  
显示所选列的数据类型。  
  
**长度**  
显示所选列的数据类型允许的字符数或位数。 此属性仅可用于基于字符的数据类型。  
  
> [!NOTE]  
> 有关以字节为单位的大小信息，请参阅下面的“大小”属性。  
  
**精度**  
显示数值数据类型所允许的最大位数。 对于非数值数据类型，此属性显示 **0** 。  
  
**小数位数**  
显示数值数据类型的小数点右侧可显示的最大位数。 此值必须小于或等于精度。 对于非数值数据类型，此属性显示 **0** 。  
  
**大小**  
显示列的数据类型允许的大小（字节）。 例如，某个 nchar 数据类型的长度为 10（字符数），但在 Unicode 字符集中，该数据类型的大小为 20。  
  
