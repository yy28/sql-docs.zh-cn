---
title: Azure Data Lake Store 文件系统任务 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 69a521cb72e68141f5706f5187a0288a3f44f241
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061378"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 文件系统任务

**Azure Data Lake Store 文件系统任务**使用户能够在[Azure Data Lake Store （ADLS）](https://azure.microsoft.com/services/data-lake-store/)上执行各种文件系统操作。

若要将 Azure Data Lake Store 文件系统任务添加到某个包，请将它从 SSIS 工具箱拖到设计器画布中。 然后双击该任务，或右键单击该任务，然后选择 "**编辑**"，以打开 "任务编辑器" 对话框。

“操作”  属性指定要执行的文件系统操作。 支持下列操作:

* **CopyToADLS：** 将文件上载到 ADLS。
* **CopyFromADLS：** 从 ADLS 下载文件。

对任何操作都必须指定 Azure Data Lake 连接管理器。

下面是特定于每个操作的属性的说明。

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory：** 指定包含要上载的文件的源目录。
* **FileNamePattern：** 指定源文件的文件名筛选器。 仅上传名称与指定模式匹配的文件。 支持 `*` 和 `?` 通配符。
* **SearchRecursively：** 指定是否在源目录中以递归方式搜索要上载的文件。
* **AzureDataLakeDirectory：** 指定要将文件上载到的 ADLS 目标目录。
* **FileExpiry：** 为上载到 ADLS 的文件指定过期日期和时间，或将此属性保留为空，以指示文件永不过期。

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory：** 指定包含待下载文件的 ADLS 源目录。
* **SearchRecursively：** 指定是否在源目录中以递归方式搜索要下载的文件。
* **LocalDirectory：** 指定要存储已下载文件的目标目录。
