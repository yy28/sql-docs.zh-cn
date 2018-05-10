---
title: 编程 AMO 互补类和方法 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8972d0659180558689302c77994f0c14f931593d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="programming-amo-complementary-classes-and-methods"></a>AMO 补充类和方法的编程
  本主题包含以下各节：  
  
-   [程序集类](#Assembly)  
  
-   [备份和还原](#BU)  
  
-   [Trace 类](#TRC)  
  
-   [CaptureLog 类和 CaptureXML 属性](#CL)  
  
##  <a name="Assembly"></a> 程序集类  
 程序集让扩展的功能的用户[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]通过添加新的存储的过程或多维表达式 (MDX) 函数。 有关详细信息，请参阅[AMO 其他类和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)。  
  
 添加和删除程序集很简单，可以联机执行。 只有数据库管理员才能向数据库添加程序集，只有服务器管理员才能向服务器对象添加程序集。  
  
 下面的示例向所提供的数据库添加一个程序集，并指定运行该程序集的服务帐户。 如果数据库中已经存在该程序集，则会先删除该程序集，然后再尝试添加。  
  
```  
static public void CreateStoredProcedures(Database db)  
{  
    ClrAssembly clrAssembly;  
  
    // Verify That assembly exist in database and drop it  
    if (db.Assemblies.ContainsName("StoredProcedures"))  
    {  
        clrAssembly = db.Assemblies.FindByName("StoredProcedures");  
        clrAssembly.Drop();  
    }  
  
    // Create the CLR assembly  
    clrAssembly = db.Assemblies.Add("StoredProcedures");  
    clrAssembly.ImpersonationInfo = new ImpersonationInfo(  
        ImpersonationMode.ImpersonateServiceAccount);  
    clrAssembly.PermissionSet = PermissionSet.Unrestricted;  
  
    // Load the assembly files  
    clrAssembly.LoadFiles(Environment.CurrentDirectory  
        + @"\StoredProcedures2.dll", false);  
  
    clrAssembly.Update();  
}  
  
```  
  
##  <a name="BU"></a> 备份和还原方法  
 Backup 和 Restore 方法供管理员用于备份和还原数据库。  
  
 下面的示例为指定服务器中的所有数据库创建备份。 如果备份文件已存在，则会覆盖该文件。 备份文件将保存到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Data 文件夹中的 BackUp 文件夹中。  
  
```  
static public void BackUpAllDatabases(Server svr)  
{  
    string fileName;  
    if ((svr != null) && ( svr.Connected))  
        foreach (Database db in svr.Databases)  
        {  
            fileName = db.Name + "_" + ((Int64)(DateTime.Today.Year * 10000 + DateTime.Today.Month * 100 + DateTime.Today.Day)).ToString()+ ".abf";  
            db.Backup(fileName, true);  
        }  
}  
```  
  
 下面的示例还原上面示例中的“Adventure Works”备份。 如果“My Adventure WorksDW”数据库已存在，则覆盖该数据库。  
  
```  
static public void RestoreAdventureWorks(Server svr)  
{  
    svr.Restore("Adventure Works DW_20051025.abf", "My Adventure WorksDW", true);  
}  
```  
  
##  <a name="TRC"></a> Trace 类  
 监视服务器活动需要使用两种跟踪：会话跟踪和服务器跟踪。 通过跟踪服务器，可以了解当前任务在服务器中的执行情况（会话跟踪），或者在不连接到服务器的情况下即可了解服务器中的总体活动情况（服务器跟踪）。  
  
 跟踪当前活动（会话跟踪）时，服务器会向当前应用程序发送有关服务器中正在发生的由该应用程序引发的事件的通知。 在当前应用程序中，使用事件处理程序来捕获事件。 首先应为 <xref:Microsoft.AnalysisServices.SessionTrace> 对象指定事件处理例程，然后启动会话跟踪。  
  
 下面的示例演示如何设置会话跟踪以跟踪当前活动。 事件处理程序例程位于示例的末尾，它会向 System.Console 对象输出所有跟踪信息。 为了生成跟踪事件，会在跟踪启动后对“Adventure Works”示例多维数据集进行全面处理。  
  
```  
static public void TestSessionTraces(Server svr)  
{  
    // Start the default trace  
  
    svr.SessionTrace.OnEvent  
        += new TraceEventHandler(DefaultTrace_OnEvent);  
    svr.SessionTrace.Stopped  
        += new TraceStoppedEventHandler(DefaultTrace_Stopped);  
    svr.SessionTrace.Start();  
  
    // Process the databases  
    // The trace handlers will output all progress notifications   
    // to the console  
    Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    cube.Process(ProcessType.ProcessFull);  
  
    // Stop the default trace  
    svr.SessionTrace.Stop();  
  
}  
static public void DefaultTrace_OnEvent(object sender, TraceEventArgs e)  
{  
    Console.WriteLine("{0}", e.TextData);  
}  
  
static public void DefaultTrace_Stopped(ITrace sender, TraceStoppedEventArgs e)  
{  
    switch (e.StopCause)  
    {  
        case TraceStopCause.StoppedByUser:  
        case TraceStopCause.Finished:  
            Console.WriteLine("Processing completed successfully");  
            break;  
  
        case TraceStopCause.StoppedByException:  
            Console.WriteLine("Processing failed: {0}",  
                e.Exception.Message);  
            break;  
    }  
}  
```  
  
 服务器跟踪可配置为向跟踪文件记录所有信息，还可以在服务重新启动时自动重新启动。  
  
 若要设置服务器跟踪，首先需要定义要监视服务器中的哪些事件，以及应将哪些事件数据保存到跟踪文件中。 对于每个事件，必须定义要保存到跟踪文件中的数据列。  
  
 创建服务器跟踪需要完成四个步骤：  
  
1.  创建服务器跟踪对象并填充基本通用属性。  
  
     LogFileSize 定义跟踪文件的最大大小，以 MB 为单位；LogFileRollOver 设定在达到 LogFileSize 限制时，可启动另一个文件作为日志文件，启用该属性后，文件名后会追加一个序列号；AutoRestart 设定在服务重新启动时，跟踪也重新启动。  
  
2.  创建事件和相应的数据列。  
  
3.  根据需要启动和停止跟踪。  
  
     即使已停止跟踪后，跟踪服务器中存在，应重新启动，如果跟踪已定义为自动重新启动 =**true**。  
  
4.  不再需要时，删除跟踪。  
  
 在下面的示例中，如果跟踪已存在，则将其删除，然后重新创建。 跟踪文件保存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Data 文件夹的 Log 文件夹中。  
  
```  
static public void TestServerTraces(Server svr)  
{  
    Trace trc;  
    TraceEvent te;  
  
        trc = svr.Traces.FindByName("TestServerTraces");  
        if (trc != null)  
            trc.Drop();  
        trc = svr.Traces.Add("TestServerTraces", "TestServerTraces");  
        trc.LogFileName = ("TestServerTraces_" +((Int64)(DateTime.Now.Year * 10000 + DateTime.Now.Month * 100 + DateTime.Now.Day)).ToString() + "_" +  
                ((Int64)(DateTime.Now.Hour * 10000 + DateTime.Now.Minute * 100 + DateTime.Now.Second)).ToString() + ".trc");  
        trc.LogFileSize = 100;  
        trc.LogFileRollover = true;  
        trc.AutoRestart = false;  
  
        #region Define Events to trace & data columns per event  
        te = trc.Events.Add(TraceEventClass.ProgressReportBegin);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportCurrent);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportEnd);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.EndTime);  
        te.Columns.Add(TraceColumn.Success);  
        te.Columns.Add(TraceColumn.Error);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
        #endregion  
  
        trc.Update();  
        trc.Start();  
  
        #region Process the Adventure Works Cube  
        // The trace settings will output all progress notifications   
        // to the trace file  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        Cube cube = db.Cubes.FindByName("Adventure Works");  
        cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        trc.Stop();  
        trc.Drop();  
  
}  
```  
  
##  <a name="CL"></a> CaptureLog 和 CaptureXml 属性  
 CaptureLog 属性设定可以基于 AMO 操作创建 XMLA 批处理文件。 CaptureLog 还设定可以在脚本中，将服务器对象编写为数据库、多维数据集、维度、挖掘结构等。  
  
 创建 CaptureLog 需要执行下列步骤：  
  
1.  开始将服务器设置捕获 XMLA 日志属性到 CaptureXml **true**。  
  
     此选项会开始将所有 AMO 操作保存到一个字符串集合中，而不会将它们发送到服务器。  
  
2.  照常启动 AMO 活动，但请注意，不会向服务器发送任何操作。 活动可为任何操作（如处理、创建、删除、更新），或对对象的任何其他操作。  
  
3.  停止通过重置到 CaptureXml 捕获 XMLA 日志**false**。  
  
4.  通过查看 CaptureLog 字符串集合中的每个字符串或使用 ConcatenateCaptureLog 方法生成一个完整的字符串来查看所捕获的 XMLA。 ConcatenateCaptureLog 可用于将 XMLA 批处理生成为单个事务，并向该批处理添加并行处理选项。  
  
 下面的示例使用批处理命令对 [Adventure Works DW Multidimensional 2012] 数据库中的所有维度和所有多维数据集进行完整处理，返回一个字符串。  
  
```  
static public string TestCaptureLog(Server svr)  
{  
    String capturedXmla = "";  
    if ((svr != null) && (svr.Connected))  
    {  
        svr.CaptureXml = true;  
  
        #region Actions to be captured to an XMLA file  
        //No action is executed during CaptureXml = true  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        foreach (Dimension dim in db.Dimensions)  
            dim.Process(ProcessType.ProcessFull);  
        foreach (Cube cube in db.Cubes)  
            cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        svr.CaptureXml = false;  
  
        capturedXmla = svr.ConcatenateCaptureLog(true, true);  
  
    }  
  
    return capturedXmla;  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 其他类和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)   
 [逻辑体系结构 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
