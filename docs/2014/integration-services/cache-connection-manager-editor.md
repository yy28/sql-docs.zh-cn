---
title: 缓存连接管理器编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cacheconnection.f1
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d22744bd83daa70994e552965ea96d148800afef
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439144"
---
# <a name="cache-connection-manager-editor"></a>缓存连接管理器编辑器
  缓存连接管理器从缓存转换或缓存文件 (.caw) 中读取引用数据集，并且可以将数据保存到缓存文件中。 这些数据始终存储在内存中。  
  
> [!NOTE]  
>  缓存连接管理器不支持二进制大型对象 (BLOB) 数据类型 DT_TEXT、DT_NTEXT 和 DT_IMAGE。 如果引用数据集包含 BLOB 数据类型，则运行包时该组件将失败。 可以使用 **“缓存连接管理器编辑器”** 修改列数据类型。  
  
 查找转换在引用数据集上执行查找。  
  
 “缓存连接管理器编辑器”**** 对话框包含以下选项卡：  
  
-   [“常规”选项卡](#generaltab)  
  
-   [列选项卡](#columnstab)  
  
 若要了解有关缓存连接管理器的详细信息，请参阅[缓存连接管理器](connection-manager/cache-connection-manager.md)。  
  
##  <a name="general-tab"></a><a name="generaltab"></a>常规选项卡  
 “缓存连接管理器编辑器”对话框的“常规”选项卡用于指示是从文件读取缓存还是将缓存保存到文件********。  
  
### <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的缓存连接提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中显示。  
  
 **说明**  
 描述此连接。 最好根据连接的用途对其进行说明，以使包的说明一目了然，且更便于维护。  
  
 **使用文件缓存**  
 指示是否使用缓存文件。  
  
> [!NOTE]  
>  包的保护级别不适用于缓存文件。 如果缓存文件包含敏感信息，可使用访问控制列表 (ACL) 来限制对存储该文件的位置或文件夹的访问。 应只允许访问某些帐户。 有关详细信息，请参阅[访问包使用的文件](../../2014/integration-services/access-to-files-used-by-packages.md)。  
  
 如果将缓存连接管理器配置为使用缓存文件，则连接管理器将执行下列操作之一：  
  
-   若将“缓存转换”转换配置为将数据从数据流中的某个数据源写入缓存连接管理器，则将数据保存到该文件。 有关详细信息，请参阅 [Cache Transform](data-flow/transformations/cache-transform.md)。  
  
-   从缓存文件读取数据。  
  
 **文件名**  
 键入缓存文件的路径和文件名。  
  
 **浏览**  
 定位缓存文件。  
  
 **刷新元数据**  
 删除缓存连接管理器中的列元数据，然后用所选缓存文件中的列元数据重新填充缓存连接管理器。  
  
##  <a name="columns-tab"></a><a name="columnstab"></a>列选项卡  
 **“缓存连接管理器编辑器”** 对话框的 **“列”** 选项卡用于配置缓存中各列的属性。  
  
### <a name="options"></a>选项  
 **列**  
 指定列名。  
  
 **索引位置**  
 通过指定各列的索引位置指定哪些列是索引列。 索引是一列或多个列的集合。  
  
 对于非索引列，索引位置是 0。  
  
 对于索引列，索引位置是连续的正数。 此数字指示查找转换将引用数据集中的行与输入数据源中的行进行比较的顺序。 具有最多唯一值的列应当具有最低的索引位置。  
  
> [!NOTE]  
>  当将查找转换配置为使用缓存连接管理器时，则仅引用数据集中的索引列能够映射到输入列。 此外，还必须对所有索引列进行映射。  
  
 **Type**  
 指定列的数据类型。  
  
 `Length`  
 指定列数据类型。 如果适用于该数据类型，则可更新`Length`。  
  
 `Precision`  
 指定特定列数据类型的精度。 精度指数字的位数。 如果适用于该数据类型，则可更新`Precision`。  
  
 `Scale`  
 指定特定列数据类型的小数位数。 小数位数指小数点后的数字位数。 如果适用于该数据类型，则可更新`Scale`。  
  
 `Code Page`  
 指定列类型的代码页。 如果适用于该数据类型，则可更新`Code Page`。  
  
## <a name="see-also"></a>另请参阅  
 [查找转换](data-flow/transformations/lookup-transformation.md)  
  
  
