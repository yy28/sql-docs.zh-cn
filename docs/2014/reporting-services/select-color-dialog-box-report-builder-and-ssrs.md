---
title: 选择颜色对话框 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.selectcolor.f1
- "10090"
helpviewer_keywords:
- Select Color dialog box
ms.assetid: ac7089a3-5c7b-4f53-8348-180610e86da2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6bcbbe828da811ace5df4feea5cfdf888e1e6ca5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101374"
---
# <a name="select-color-dialog-box-report-builder-and-ssrs"></a>“选择颜色”对话框（报表生成器和 SSRS）
  使用 **“选择颜色”** 对话框可以为数据区域或文本框中单个或多个单元的背景指定颜色选项，或为图表指定颜色选项。  
  
## <a name="options"></a>选项  
 **颜色选择器**  
 从三个用于指定颜色选择方式的选项中进行选择：  
  
-   **选取器 - 色环** 使用“色调/饱和度/亮度”(HSB) 颜色值选择颜色。  
  
-   **选取器 - 色块** 使用“红/绿/蓝”(RGB) 颜色值选择颜色。  
  
-   **调色板 - 标准颜色** 从预定义的颜色值列表中选择颜色。  
  
 **色环**  
 用于 HSB 颜色，因为 HSB 值映射到柱面坐标系。 色调是实际的颜色，饱和度是颜色纯度，亮度是相对的明暗。  
  
 当您选取一个颜色时，圆的中心决定了颜色。 使用颜色滑块可更改色调。 x 坐标和 y 坐标分别表示饱和度和亮度值。  
  
 **色块**  
 用于 RGB 颜色，因为 RGB 值映射到笛卡尔坐标系。 R 代表红色值，G 代表绿色值，B 代表蓝色值。  
  
 当您选取一个颜色时，方块的中心决定了颜色。 使用颜色滑块可更改所选颜色的范围。 x 和 y 坐标代表其他两种颜色。 例如，如果您选择绿色，滑块将显示绿色值的范围，x 和 y 坐标则分别代表红色和蓝色值。  
  
 **标准调色板颜色**  
 用于中的命名颜色[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]`KnownColor`枚举。  
  
 **颜色系统**  
 指定 RGB 或 HSB 颜色。 该选项用于更改显示器以显示 RGB 或 HSB 值，当您使用 **“颜色选择器”** 的色环或色块时，这些值将以交互方式更新。  
  
 对于某些属性，如果颜色可包含透明度值，则会显示 **Alpha** 值。 例如，图表序列填充。 对于不支持透明度的属性，该值将被禁用。  
  
 **Red**  
 代表 RGB 颜色中红色部分的十进制值。 使用数字调整框可更改值或键入一个介于 0 到 255 之间的值。  
  
 **绿色**  
 代表 RGB 颜色中绿色部分的十进制值。 使用数字调整框可更改值或键入一个介于 0 到 255 之间的值。  
  
 **蓝色**  
 代表 RGB 颜色中蓝色部分的十进制值。 使用数字调整框可更改值或键入一个介于 0 到 255 之间的值。  
  
 **Alpha**  
 代表颜色中 Alpha 或透明度部分的十进制值。 启用该值后，您可使用滑块开关调整至所需的透明度。  
  
 **色调**  
 代表 HSB 颜色色调的十进制值。 使用数字调整框可更改值或键入一个介于 0 到 255 之间的值。  
  
 **饱和度**  
 代表 HSB 颜色饱和度的十进制值。 使用数字调整框可更改值或键入一个介于 0 到 255 之间的值。  
  
 **亮度**  
 代表 HSB 颜色亮度的十进制值。 使用数字调整框可更改值或键入一个介于 0 到 255 之间的值。  
  
 **颜色示例**  
 在窗格的左半部分显示当前颜色，并在窗格的右半部分以交互方式显示您所选择的新颜色。 如果没有默认颜色，窗格的左半部分为白色。 绝大多数 RDL 属性没有默认颜色。  
  
## <a name="see-also"></a>请参阅  
 [设置报表项的格式（报表生成器和 SSRS）](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [设置文本和占位符的格式（报表生成器和 SSRS）](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
