---
title: Mscorlib.dll 中禁用的类型和成员 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: daf82d4b-2f6d-44ca-9148-75193321b6d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 43f71d7dc73239b240b841e14a11f3f28f755b61
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874357"
---
# <a name="disallowed-types-and-members-in-mscorlibdll"></a>mscorlib.dll 中禁用的类型和成员
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共`HostProtectionAttribute`语言集成（CLR）编程不允许使用具有`System.Security.Permissions.HostProtectionResource` `ExternalProcessMgmt`、 `ExternalThreading` `MayLeakOnAbort` `SecurityInfrastructure` `SelfAffectingProcessMgmnt` `SelfAffectingThreading`、、、、、、 **SharedState**、 `Synchronization`或`UI`的值的类型或成员。 下表列出了宿主保护属性 (HPA) 值被禁用的 mscorlib.dll 程序集的成员和类型。  
  
> [!NOTE]  
>  此列表是通过支持的程序集生成的。 有关详细信息，请参阅[支持的 .NET Framework 库](../clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|类型或成员|HPA 值|  
|--------------------|--------------------|  
|SyncStream.BeginRead()|ExternalThreading|  
|SyncStream.BeginWrite()|ExternalThreading|  
|System.Collections.ArrayList.Synchronized()|Synchronization|  
|System.Collections.Hashtable.Synchronized()|Synchronization|  
|System.Collections.Queue.Synchronized()|Synchronization|  
|System.Collections.SortedList.Synchronized()|Synchronization|  
|System.Collections.Stack.Synchronized()|Synchronization|  
|System.Console.Beep()|UI|  
|System.Console.get_Error()|UI|  
|System.Console.get_In()|UI|  
|System.Console.get_KeyAvailable()|UI|  
|System.Console.get_Out()|UI|  
|System.Console.OpenStandardError()|UI|  
|System.Console.OpenStandardInput()|UI|  
|System.Console.OpenStandardOutput()|UI|  
|System.Console.Read()|UI|  
|System.Console.ReadKey()|UI|  
|System.Console.ReadLine()|UI|  
|System.Console.SetError()|UI|  
|System.Console.SetIn()|UI|  
|System.Console.SetOut()|UI|  
|System.Console.Write()|UI|  
|System.Console.WriteLine()|UI|  
|System.Diagnostics.LogMessageEventHandler|ExternalThreading，Synchronization|  
|System.IO.FileStream.BeginRead()|ExternalThreading|  
|System.IO.FileStream.BeginWrite()|ExternalThreading|  
|System.IO.Stream.Synchronized()|Synchronization|  
|System.IO.TextReader.Synchronized()|Synchronization|  
|System.IO.TextWriter.Synchronized()|Synchronization|  
|System.Reflection.Emit.AssemblyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.ConstructorBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.CustomAttributeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EnumBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EventBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.FieldBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodRental|MayLeakOnAbort|  
|System.Reflection.Emit.ModuleBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.PropertyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.TypeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.UnmanagedMarshal|MayLeakOnAbort|  
|System.Security.Principal.WindowsPrincipal|SecurityInfrastructure|  
|System.Threading.AutoResetEvent|ExternalThreading，Synchronization|  
|System.Threading.EventWaitHandle|ExternalThreading，Synchronization|  
|System.Threading.ManualResetEvent|ExternalThreading，Synchronization|  
|System.Threading.Monitor|ExternalThreading，Synchronization|  
|System.Threading.Mutex|ExternalThreading，Synchronization|  
|System.Threading.ReaderWriterLock|ExternalThreading，Synchronization|  
|System.Threading.Thread.AllocateDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.AllocateNamedDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.BeginCriticalRegion()|ExternalThreading，Synchronization|  
|System.Threading.Thread.EndCriticalRegion()|ExternalThreading，Synchronization|  
|System.Threading.Thread.FreeNamedDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.GetData()|ExternalThreading，SharedState|  
|System.Threading.Thread.GetNamedDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.Join()|ExternalThreading，Synchronization|  
|System.Threading.Thread.set_ApartmentState()|Synchronization，SelfAffectingThreading|  
|System.Threading.Thread.set_CurrentUICulture()|ExternalThreading|  
|System.Threading.Thread.set_IsBackground()|SelfAffectingThreading|  
|System.Threading.Thread.set_Name()|ExternalThreading|  
|System.Threading.Thread.set_Priority()|SelfAffectingThreading|  
|System.Threading.Thread.SetApartmentState()|Synchronization，SelfAffectingThreading|  
|System.Threading.Thread.SetData()|ExternalThreading，SharedState|  
|System.Threading.Thread.SpinWait()|ExternalThreading，Synchronization|  
|System.Threading.Thread.Start()|ExternalThreading，Synchronization|  
|System.Threading.Thread.TrySetApartmentState()|Synchronization，SelfAffectingThreading|  
|System.Threading.ThreadPool|ExternalThreading，Synchronization|  
|System.Threading.Timer|ExternalThreading，Synchronization|  
|System.Threading.TimerBase|ExternalThreading，Synchronization|  
  
## <a name="see-also"></a>另请参阅  
 [宿主保护属性和 CLR 集成编程](host-protection-attributes-and-clr-integration-programming.md)   
 [不允许的类型和成员在](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [系统中不允许的类型和成员](disallowed-types-and-members-in-system-dll.md)   
 [系统中不允许的类型和成员](disallowed-types-and-members-in-system-data-dll.md)   
 [System.Core.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-core-dll.md)  
  
  
