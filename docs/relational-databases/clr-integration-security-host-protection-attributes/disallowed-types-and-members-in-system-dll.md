---
title: No se permiten tipos y miembros en System.dll | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: 27b550cd-dd3d-4263-bd97-0f0dec1215fd
author: rothja
ms.author: jroth
ms.openlocfilehash: ea48198bba845da74b82b2a7748c1e6bf2ed8692
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028071"
---
# <a name="disallowed-types-and-members-in-systemdll"></a>Disallowed Types and Members In System.dll
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programación de Common language integration (CLR) no permite el uso de un tipo o miembro que tiene un **HostProtectionAttribute** que especifica un **System.Security.Permissions.HostProtectionResource** enumeración con un valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **sincronización**, o **UI**. En la tabla siguiente se enumeran los miembros y tipos del ensamblado System.dll cuyos valores de atributo de protección de host (HPA) no están permitidos.  
  
> [!NOTE]  
>  Esta lista se generó a partir de los ensamblados admitidos. Para obtener más información, consulte [admite bibliotecas de .NET Framework](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o miembro|Valores de HPA|  
|--------------------|--------------------|  
|Microsoft.Win32.NativeMethods|MayLeakOnAbort|  
|Microsoft.Win32.PowerModeChangedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.PowerModeChangedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventLogReadHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventLogWriteHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeFileMappingHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeFileMapViewHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeLibraryHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeLocalMemHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeProcessHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeUserTokenHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeNativeMethods|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndingEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndingEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SessionSwitchEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.SessionSwitchEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SystemEvents|MayLeakOnAbort|  
|Microsoft.Win32.TimerElapsedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.TimerElapsedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.UnsafeNativeMethods|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangingEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangingEventHandler|MayLeakOnAbort|  
|System.ComponentModel.AddingNewEventArgs|SharedState|  
|System.ComponentModel.AddingNewEventHandler|SharedState|  
|System.ComponentModel.ArrayConverter|SharedState|  
|System.ComponentModel.ArraySubsetEnumerator|SharedState|  
|System.ComponentModel.AsyncCompletedEventArgs|SharedState|  
|System.ComponentModel.AsyncCompletedEventHandler|SharedState|  
|System.ComponentModel.AsyncOperation|SharedState|  
|System.ComponentModel.AsyncOperationManager|SharedState|  
|System.ComponentModel.AttributeCollection|Sincronización|  
|System.ComponentModel.BackgroundWorker|SharedState|  
|System.ComponentModel.BaseNumberConverter|SharedState|  
|System.ComponentModel.BindingList|SharedState|  
|System.ComponentModel.BooleanConverter|SharedState|  
|System.ComponentModel.ByteConverter|SharedState|  
|System.ComponentModel.CancelEventArgs|SharedState|  
|System.ComponentModel.CancelEventHandler|SharedState|  
|System.ComponentModel.CharConverter|SharedState|  
|System.ComponentModel.CollectionChangeEventArgs|SharedState|  
|System.ComponentModel.CollectionChangeEventHandler|SharedState|  
|System.ComponentModel.CollectionConverter|SharedState|  
|System.ComponentModel.CompModSwitches|SharedState|  
|System.ComponentModel.ComponentCollection|Sincronización|  
|System.ComponentModel.ComponentConverter|SharedState|  
|System.ComponentModel.ComponentEditor|SharedState|  
|System.ComponentModel.ComponentResourceManager|SharedState|  
|System.ComponentModel.Container|SharedState|  
|System.ComponentModel.ContainerFilterService|SharedState|  
|System.ComponentModel.CultureInfoConverter|SharedState|  
|System.ComponentModel.CustomTypeDescriptor|SharedState|  
|System.ComponentModel.DateTimeConverter|SharedState|  
|System.ComponentModel.DecimalConverter|SharedState|  
|System.ComponentModel.DelegatingTypeDescriptionProvider|SharedState|  
|System.ComponentModel.Design.ActiveDesignerEventArgs|SharedState|  
|System.ComponentModel.Design.ActiveDesignerEventHandler|SharedState|  
|System.ComponentModel.Design.CheckoutException|SharedState|  
|System.ComponentModel.Design.CommandID|SharedState|  
|System.ComponentModel.Design.ComponentChangedEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentChangedEventHandler|SharedState|  
|System.ComponentModel.Design.ComponentChangingEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentChangingEventHandler|SharedState|  
|System.ComponentModel.Design.ComponentEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentEventHandler|SharedState|  
|System.ComponentModel.Design.ComponentRenameEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentRenameEventHandler|SharedState|  
|System.ComponentModel.Design.DesignerCollection|SharedState|  
|System.ComponentModel.Design.DesignerEventArgs|SharedState|  
|System.ComponentModel.Design.DesignerEventHandler|SharedState|  
|System.ComponentModel.Design.DesignerOptionService|SharedState|  
|System.ComponentModel.Design.DesignerTransaction|SharedState|  
|System.ComponentModel.Design.DesignerTransactionCloseEventArgs|SharedState|  
|System.ComponentModel.Design.DesignerTransactionCloseEventHandler|SharedState|  
|System.ComponentModel.Design.DesignerVerb|SharedState|  
|System.ComponentModel.Design.DesignerVerbCollection|SharedState|  
|System.ComponentModel.Design.DesigntimeLicenseContext|SharedState|  
|System.ComponentModel.Design.DesigntimeLicenseContextSerializer|SharedState|  
|System.ComponentModel.Design.MenuCommand|SharedState|  
|System.ComponentModel.Design.RuntimeLicenseContext|SharedState|  
|System.ComponentModel.Design.Serialization.ComponentSerializationService|SharedState|  
|System.ComponentModel.Design.Serialization.ContextStack|SharedState|  
|System.ComponentModel.Design.Serialization.DesignerLoader|SharedState|  
|System.ComponentModel.Design.Serialization.InstanceDescriptor|SharedState|  
|System.ComponentModel.Design.Serialization.MemberRelationshipService|SharedState|  
|System.ComponentModel.Design.Serialization.ResolveNameEventArgs|SharedState|  
|System.ComponentModel.Design.Serialization.ResolveNameEventHandler|SharedState|  
|System.ComponentModel.Design.Serialization.SerializationStore|SharedState|  
|System.ComponentModel.Design.ServiceContainer|SharedState|  
|System.ComponentModel.Design.ServiceCreatorCallback|SharedState|  
|System.ComponentModel.Design.StandardCommands|SharedState|  
|System.ComponentModel.Design.StandardToolWindows|SharedState|  
|System.ComponentModel.DoubleConverter|SharedState|  
|System.ComponentModel.DoWorkEventArgs|SharedState|  
|System.ComponentModel.DoWorkEventHandler|SharedState|  
|System.ComponentModel.EnumConverter|SharedState|  
|System.ComponentModel.EventDescriptor|SharedState|  
|System.ComponentModel.EventDescriptorCollection|Sincronización|  
|System.ComponentModel.EventHandlerList|SharedState|  
|System.ComponentModel.ExpandableObjectConverter|SharedState|  
|System.ComponentModel.ExtendedPropertyDescriptor|SharedState|  
|System.ComponentModel.GuidConverter|SharedState|  
|System.ComponentModel.HandledEventArgs|SharedState|  
|System.ComponentModel.HandledEventHandler|SharedState|  
|System.ComponentModel.InstanceCreationEditor|SharedState|  
|System.ComponentModel.Int16Converter|SharedState|  
|System.ComponentModel.Int32Converter|SharedState|  
|System.ComponentModel.Int64Converter|SharedState|  
|System.ComponentModel.IntSecurity|SharedState|  
|System.ComponentModel.InvalidAsynchronousStateException|SharedState|  
|System.ComponentModel.InvalidEnumArgumentException|SharedState|  
|System.ComponentModel.ISynchronizeInvoke.BeginInvoke ()|ExternalThreading, Synchronization|  
|System.ComponentModel.License|SharedState|  
|System.ComponentModel.LicenseContext|SharedState|  
|System.ComponentModel.LicenseException|SharedState|  
|System.ComponentModel.LicenseManager|ExternalProcessMgmt|  
|System.ComponentModel.LicenseProvider|SharedState|  
|System.ComponentModel.LicFileLicenseProvider|SharedState|  
|System.ComponentModel.ListChangedEventArgs|SharedState|  
|System.ComponentModel.ListChangedEventHandler|SharedState|  
|System.ComponentModel.ListSortDescription|SharedState|  
|System.ComponentModel.ListSortDescriptionCollection|SharedState|  
|System.ComponentModel.MaskedTextProvider|SharedState|  
|System.ComponentModel.MemberDescriptor|SharedState|  
|System.ComponentModel.MultilineStringConverter|SharedState|  
|System.ComponentModel.NestedContainer|SharedState|  
|System.ComponentModel.NullableConverter|SharedState|  
|System.ComponentModel.ProgressChangedEventArgs|SharedState|  
|System.ComponentModel.ProgressChangedEventHandler|SharedState|  
|System.ComponentModel.PropertyChangedEventArgs|SharedState|  
|System.ComponentModel.PropertyChangedEventHandler|SharedState|  
|System.ComponentModel.PropertyDescriptor|SharedState|  
|System.ComponentModel.PropertyDescriptorCollection|Sincronización|  
|System.ComponentModel.ReferenceConverter|SharedState|  
|System.ComponentModel.ReflectEventDescriptor|SharedState|  
|System.ComponentModel.ReflectPropertyDescriptor|SharedState|  
|System.ComponentModel.ReflectTypeDescriptionProvider|SharedState|  
|System.ComponentModel.RefreshEventArgs|SharedState|  
|System.ComponentModel.RefreshEventHandler|SharedState|  
|System.ComponentModel.RunWorkerCompletedEventArgs|SharedState|  
|System.ComponentModel.RunWorkerCompletedEventHandler|SharedState|  
|System.ComponentModel.SByteConverter|SharedState|  
|System.ComponentModel.SingleConverter|SharedState|  
|System.ComponentModel.StringConverter|SharedState|  
|System.ComponentModel.SyntaxCheck|SharedState|  
|System.ComponentModel.TimeSpanConverter|SharedState|  
|System.ComponentModel.TypeConverter|SharedState|  
|System.ComponentModel.TypeDescriptionProvider|SharedState|  
|System.ComponentModel.TypeDescriptor|SharedState|  
|System.ComponentModel.TypeListConverter|SharedState|  
|System.ComponentModel.UInt16Converter|SharedState|  
|System.ComponentModel.UInt32Converter|SharedState|  
|System.ComponentModel.UInt64Converter|SharedState|  
|System.ComponentModel.WarningException|SharedState|  
|System.ComponentModel.WeakHashtable|SharedState|  
|System.ComponentModel.Win32Exception|SharedState|  
|System.Diagnostics.ConsoleTraceListener|Sincronización|  
|System.Diagnostics.Debug.get_Listeners ()|SharedState|  
|System.Diagnostics.DefaultTraceListener|Sincronización|  
|System.Diagnostics.DelimitedListTraceListener|Sincronización|  
|System.Diagnostics.EventLog.get_SynchronizingObject ()|Sincronización|  
|System.Diagnostics.EventLogTraceListener|Sincronización|  
|System.Diagnostics.PerformanceCounter|SharedState, Synchronization|  
|System.Diagnostics.PerformanceCounterCategory|SharedState, Synchronization|  
|System.Diagnostics.Process|SelfAffectingProcessMgmt, ExternalProcessMgmt, SharedState, Synchronization|  
|System.Diagnostics.ProcessStartInfo|SelfAffectingProcessMgmt, SharedState|  
|System.Diagnostics.ProcessThread|SelfAffectingThreading, SelfAffectingProcessMgmt|  
|System.Diagnostics.SharedPerformanceCounter|SharedState, Synchronization|  
|System.Diagnostics.TextWriterTraceListener|Sincronización|  
|System.Diagnostics.Trace.get_Listeners ()|SharedState|  
|System.Diagnostics.TraceListener|Sincronización|  
|System.Diagnostics.XmlWriterTraceListener|Sincronización|  
|System.IO.Compression.DeflateStream.BeginRead ()|ExternalThreading|  
|System.IO.Compression.DeflateStream.BeginWrite()|ExternalThreading|  
|System.IO.Compression.GZipStream.BeginRead ()|ExternalThreading|  
|System.IO.Compression.GZipStream.BeginWrite()|ExternalThreading|  
|System.IO.Ports.SerialStream.BeginRead ()|ExternalThreading|  
|System.IO.Ports.SerialStream.BeginWrite()|ExternalThreading|  
|System.Media.SoundPlayer|UI|  
|System.Media.SystemSound|UI|  
|System.Media.SystemSounds|UI|  
|System.Net.ConnectStream.BeginRead ()|ExternalThreading|  
|System.Net.ConnectStream.BeginWrite ()|ExternalThreading|  
|System.Net.Dns.BeginGetHostAddresses ()|ExternalThreading|  
|System.Net.Dns.BeginGetHostByName ()|ExternalThreading|  
|System.Net.Dns.BeginGetHostEntry ()|ExternalThreading|  
|System.Net.Dns.BeginResolve ()|ExternalThreading|  
|System.Net.FileWebRequest.BeginGetRequestStream ()|ExternalThreading|  
|System.Net.FileWebRequest.BeginGetResponse ()|ExternalThreading|  
|System.Net.FtpDataStream.BeginRead ()|ExternalThreading|  
|System.Net.FtpDataStream.BeginWrite ()|ExternalThreading|  
|System.Net.FtpWebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.FtpWebRequest.BeginGetResponse()|ExternalThreading|  
|System.Net.HttpListener.BeginGetContext ()|ExternalThreading|  
|System.Net.HttpRequestStream.BeginRead ()|ExternalThreading|  
|System.Net.HttpRequestStream.BeginWrite()|ExternalThreading|  
|System.Net.HttpResponseStream.BeginRead ()|ExternalThreading|  
|System.Net.HttpResponseStream.BeginWrite ()|ExternalThreading|  
|System.Net.HttpWebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.HttpWebRequest.BeginGetResponse()|ExternalThreading|  
|System.Net.Mail.SmtpClient.SendAsync ()|ExternalThreading|  
|System.Net.NetworkInformation.Ping.SendAsync ()|ExternalThreading|  
|System.Net.PooledStream.BeginRead ()|ExternalThreading|  
|System.Net.PooledStream.BeginWrite ()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginAuthenticateAsClient ()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginAuthenticateAsServer()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginRead ()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginWrite()|ExternalThreading|  
|System.Net.Security.SslStream.BeginAuthenticateAsClient ()|ExternalThreading|  
|System.Net.Security.SslStream.BeginAuthenticateAsServer()|ExternalThreading|  
|System.Net.Security.SslStream.BeginRead ()|ExternalThreading|  
|System.Net.Security.SslStream.BeginWrite ()|ExternalThreading|  
|System.Net.Sockets.NetworkStream.BeginRead ()|ExternalThreading|  
|System.Net.Sockets.NetworkStream.BeginWrite()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginAccept ()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginConnect ()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginDisconnect()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginReceive ()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginReceiveFrom()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginSend ()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginSendFile()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginSendTo()|ExternalThreading|  
|System.Net.Sockets.TcpClient.BeginConnect ()|ExternalThreading|  
|System.Net.Sockets.TcpListener.BeginAcceptSocket ()|ExternalThreading|  
|System.Net.Sockets.TcpListener.BeginAcceptTcpClient ()|ExternalThreading|  
|System.Net.Sockets.UdpClient.BeginReceive ()|ExternalThreading|  
|System.Net.Sockets.UdpClient.BeginSend ()|ExternalThreading|  
|System.Net.SpnDictionary.get_SyncRoot ()|Sincronización|  
|System.Net.WebClient.DownloadDataAsync ()|ExternalThreading|  
|System.Net.WebClient.DownloadFileAsync()|ExternalThreading|  
|System.Net.WebClient.DownloadStringAsync ()|ExternalThreading|  
|System.Net.WebClient.OpenReadAsync ()|ExternalThreading|  
|System.Net.WebClient.OpenWriteAsync ()|ExternalThreading|  
|System.Net.WebClient.UploadDataAsync()|ExternalThreading|  
|System.Net.WebClient.UploadFileAsync()|ExternalThreading|  
|System.Net.WebClient.UploadStringAsync ()|ExternalThreading|  
|System.Net.WebClient.UploadValuesAsync ()|ExternalThreading|  
|System.Net.WebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.WebRequest.BeginGetResponse()|Sincronización|  
|System.Text.RegularExpressions.Group.Synchronized ()|Sincronización|  
|System.Text.RegularExpressions.Match.Synchronized ()|Sincronización|  
|System.Text.RegularExpressions.Regex.CompileToAssembly ()|MayLeakOnAbort|  
|System.Threading.Semaphore|ExternalThreading, Synchronization|  
|System.Timers.Timer|ExternalThreading, Synchronization|  
|WebClientWriteStream.BeginRead ()|ExternalThreading|  
|WebClientWriteStream.BeginWrite ()|ExternalThreading|  
  
## <a name="see-also"></a>Vea también  
 [Atributos de protección de host y programación de la integración CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Los miembros de Microsoft.VisualBasic.dll y tipos no permitidos](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos y miembros en mscorlib.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Los miembros en System.Data.dll y tipos no permitidos](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)   
 [Tipos y miembros no permitidos en System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
