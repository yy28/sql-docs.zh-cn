---
title: "catalog.add_data_tap_by_guid |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9bd4ecb4a6a419f1965a349d46d16d764dd83708
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  对于执行实例，在包数据流中将数据分流点添加到指定的数据流路径。  
  
## <a name="syntax"></a>语法  
  
```tsql  
add_data_tap_by_guid [ @execution_id = ] execution_id  
[ @dataflow_task_guid = ] dataflow_task_guid   
[ @dataflow_path_id_string = ] dataflow_path_id_string  
[ @data_filename = ] data_filename  
[ @max_rows = ] max_rows  
[ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>参数  
 [ @execution_id =] *execution_id*  
 包含包的执行 ID。 *Execution_id*是**bigint**。  
  
 [ @dataflow_task_guid =] *dataflow_task_guid*  
 包含要分流的数据流路径的包中的数据任务流 ID。 *Dataflow_task_guid*是**uniqueidentifier**。  
  
 [ @dataflow_path_id_string =] *dataflow_path_id_string*  
 数据流路径标识字符串。 一个路径连接两个数据流组件。 **IdentificationString**路径的属性指定的字符串。  
  
 要在中查找的标识字符串，[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]右键单击两个数据流组件，然后单击之间的路径**属性**。 **IdentificationString**属性将显示在**属性**窗口。  
  
 *Dataflow_path_id_string*是**nvarchar （4000)**。  
  
 [ @data_filename =] *data_filename*  
 存储分流的数据的文件名称。 如果数据流任务在 Foreach 循环或 For 循环容器内执行，则用单独的文件存储该循环每次迭代的分流数据。 用与每次迭代对应的编号为每个文件加前缀。 数据分流文件写入该文件夹"*\<SQL Server 安装文件夹 >*\130\DTS\\"。 *Data_filename*是**nvarchar （4000)**。  
  
 [ @max_rows =] max_rows  
 在数据分流期间捕获的行数。 如果未指定此值，则捕获所有行。 Max_rows 是**int**。  
  
 [ @data_tap_id =] *data_tap_id*  
 数据分流点的 ID。 *Data_tap_id*是**bigint**。  
  
## <a name="example"></a>示例  
 在下面的示例中，在数据流路径上, 创建数据分流点`Paths[SRC DimDCVentor.OLE DB Source Output]`，请在数据流任务`{D978A2E4-E05D-4374-9B05-50178A8817E8}`。 分流的数据存储在 DCVendorOutput.csv 文件中。  
  
```  
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
  
```  
  
## <a name="remarks"></a>注释  
 若要添加数据分流点，执行的实例必须在创建的状态 (值为 1 中**状态**列[catalog.operations &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)视图)。 只要运行执行，状态值就会发生更改。 您可以创建执行时通过调用[catalog.create_execution &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 以下是 add_data_tap_by_guid 存储过程的注意事项。  
  
-   添加数据分流点时，在运行包之前不进行验证。  
  
-   建议限制在数据分流期间捕获的行数，以避免生成大型数据文件。 如果执行存储过程的计算机无法为数据文件提供足够的存储空间，存储过程将停止运行。  
  
-   运行 add_data_tap_by_guid 存储过程会影响包的性能。 建议您仅运行该存储过程来解决数据问题。  
  
-   要访问存储分流数据的文件，您必须对运行该存储过程的计算机具有管理员权限，或者必须是开始执行包含带数据分流点的包的用户。  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对执行实例的 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   用户没有 MODIFY 权限。  
  
-   已添加指定的包中指定组件的数据分流点。  
  
-   为要捕获的行数指定的值无效。  
  
## <a name="requirements"></a>要求  
  
## <a name="see-also"></a>另请参阅  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  
