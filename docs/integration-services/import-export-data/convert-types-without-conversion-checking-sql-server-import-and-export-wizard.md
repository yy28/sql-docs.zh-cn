---
title: 转换类型时不进行转换检查（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.nomappingfile.f1
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e98140e69ce5ba617f1ee048648e73dbc54437b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723843"
---
# <a name="convert-types-without-conversion-checking-sql-server-import-and-export-wizard"></a>转换类型时不进行转换检查（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  选择现有表和视图进行复制或查看提供的查询之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导可能会显示“转换类型时不进行转换检查”  。 当向导找不到在源和目标之间映射数据类型所需的一个或多个数据类型转换和映射文件时，将显示此页。 此页包含的信息可帮助你了解缺少的内容。
  
 在不知道数据类型转换是否会成功的情况下，单击“下一步”  继续操作。 否则，请单击“返回”  更改选择，或单击“取消”  退出向导。

## <a name="screen-shot-of-the-convert-types-page"></a>“转换类型”页的屏幕截图  
  
下面的屏幕截图显示了向导中的“转换类型时不进行转换检查”  页的一个示例。

![转换类型](../../integration-services/import-export-data/media/convert-types.png)

此处的问题在于向导找不到映射所选目标的数据类型的映射文件。

此页上的信息不包括缺少的映射文件的名称。 由于该向导不知道用于指定的数据提供程序的文件是否存在，因此不能提供缺少的文件的名称。

## <a name="whats-next"></a>下一步是什么？  
 在不知道数据类型转换是否会成功的情况下，单击“下一步”  ，下一页是“保存并运行包”  。 在此页上，你可以指定是否要立即运行复制操作。 根据你的配置，或许还可以保存向导创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，以便对其进行自定义并在以后重新使用。 有关详细信息，请参阅 [保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
