---
title: Entwickeln von Datenflusskomponenten mit mehreren Eingaben | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 74bcf1549cdd97752c805f1c6a9cc774ef1a9e52
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384338"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>Entwickeln von Datenflusskomponenten mit mehreren Eingaben
  Eine Datenflusskomponente mit mehreren Eingaben verbraucht möglicherweise übermäßig viel Arbeitsspeicher, wenn die Eingaben unregelmäßig Daten erzeugen. Wenn Sie eine benutzerdefinierte Datenflusskomponente entwickeln, die mindestens zwei Eingaben unterstützt, können Sie diese hohe Speicherauslastung verwalten, indem Sie die folgenden Elemente im Namespace „Microsoft.SqlServer.Dts.Pipeline“ verwenden:  
  
-   Die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft der <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>-Klasse. Legen Sie den Wert dieser Eigenschaft auf `true` fest, um den Code zu implementieren, der erforderlich ist, damit die benutzerdefinierte Datenflusskomponente unregelmäßige Datenflüsse verwaltet.  
  
-   Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse. Sie müssen eine Implementierung dieser Methode bereitstellen, wenn Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft auf `true` festlegen. Wenn Sie keine Implementierung bereitstellen, löst die Datenfluss-Engine zur Laufzeit eine Ausnahme aus.  
  
-   Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse. Sie müssen auch eine Implementierung dieser Methode bereitstellen, wenn Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft auf `true` festlegen und die benutzerdefinierte Komponente mehr als zwei Eingaben unterstützt. Wenn Sie keine Implementierung bereitstellen, löst die Datenfluss-Engine zur Laufzeit eine Ausnahme aus, wenn der Benutzer mehr als zwei Eingaben anfügt.  
  
 Zusammen ermöglichen diese Elemente es Ihnen, eine Lösung für hohe Speicherauslastungen zu entwickeln, die der von Microsoft entwickelten Lösung für die Transformationen für Zusammenführen und Zusammenführungsjoin ähnelt.  
  
## <a name="setting-the-supportsbackpressure-property"></a>Festlegen der SupportsBackPressure-Eigenschaft  
 Der erste Schritt beim Implementieren einer besseren Speicherverwaltung für eine benutzerdefinierte Datenflusskomponente, die mehrere Eingaben unterstützt, besteht darin, den Wert der <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft im <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> auf `true` festzulegen. Wenn der Wert von <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>`true` ist, ruft die Datenfluss-Engine die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode auf. Bei mehr als zwei Eingaben wird außerdem die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode zur Laufzeit aufgerufen.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel legt die Implementierung von <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> den Wert von <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> auf `true` fest.  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>Implementieren der IsInputReady-Methode  
 Wenn Sie den Wert der <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft im <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>-Objekt auf `true` festlegen, müssen Sie auch eine Implementierung für die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse bereitstellen.  
  
> [!NOTE]  
>  Die Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode sollte nicht die Implementierungen in der Basisklasse aufrufen. Die Standardimplementierung dieser Methode in der Basisklasse löst lediglich eine `NotImplementedException` aus.  
  
 Wenn Sie diese Methode implementieren, legen Sie den Status eines Elements im booleschen *canProcess* -Array für jede Eingabe der Komponente fest. (Die Eingaben werden von ihren ID-Werten im *inputIDs*-Array identifiziert.) Wenn Sie legen Sie den Wert eines Elements in der *CanProcess* array an `true` für eine Eingabe, ruft die Datenfluss-Engine die Komponente des <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> Methode und stellt Sie für die angegebene Eingabe mehr Daten bereit.  
  
 Während Upstreamdaten mehr verfügbar ist, werden der Wert des der *CanProcess* Arrayelement für mindestens eine Eingabe sein `true`, oder die Verarbeitung beendet.  
  
 Die Datenfluss-Engine ruft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode vor dem Senden der einzelnen Datenpuffer auf, um zu bestimmen, welche Eingaben auf den Empfang weiterer Daten warten. Wenn der Rückgabewert angibt, dass eine Eingabe blockiert wird, speichert die Datenfluss-Engine vorübergehend zusätzliche Datenpuffer für diese Eingabe, statt sie an die Komponente zu senden.  
  
> [!NOTE]  
>  Sie rufen die Methode <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> oder <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> nicht in eigenem Code auf. Die Datenfluss-Engine ruft diese Methoden und die anderen Methoden der `PipelineComponent`-Klasse auf, die Sie überschreiben, wenn die Datenfluss-Engine die Komponente ausführt.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel gibt die Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode an, dass eine Eingabe auf den Empfang weiterer Daten wartet, wenn die folgenden Voraussetzungen erfüllt sind:  
  
-   Mehr Upstreamdaten sind für die Eingabe verfügbar (`!inputEOR`).  
  
-   Die Komponente verfügt derzeit nicht über Daten, die für die Eingabe in den Puffern verarbeitet werden können, die die Komponente bereits empfangen hat (`inputBuffers[inputIndex].CurrentRow() == null`).  
  
 Wenn eine Eingabe auf den Empfang weiterer Daten wartet, gibt die Datenflusskomponente dies festlegen, dass `true` den Wert des Elements in der *CanProcess* Array, das dieser Eingabe entspricht.  
  
 Wenn die Komponente hingegen weiterhin verfügbare Daten aufweist, die für die Eingabe verarbeitet können, wird im Beispiel die Verarbeitung der Eingabe angehalten. Hierfür wird im Beispiel `false` den Wert des Elements in der *CanProcess* Array, das dieser Eingabe entspricht.  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 Im vorangehenden Beispiel wird das boolesche `inputEOR` -Array verwendet, um anzugeben, ob für die jeweiligen Eingaben weitere Upstreamdaten verfügbar sind. `EOR` im Namen des Arrays steht für "Ende des Rowsets" und bezieht sich auf die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A>-Eigenschaft von Datenflusspuffern. In einem Teil des Beispiels, der hier nicht enthalten ist, überprüft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>-Methode den Wert der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A>-Eigenschaft für jeden empfangenen Datenpuffer. Wenn durch den Wert `true` angegeben wird, dass für eine Eingabe keine Upstreamdaten mehr verfügbar sind, wird im Beispiel der Wert des `inputEOR`-Arrayelements für diese Eingabe auf `true` festgelegt. Des in diesem Beispiel die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> Methode legt den Wert des entsprechenden Elements in der *CanProcess* array an `false` für eine Eingabe bei der der Wert des der `inputEOR` Array-Elements gibt an, dass keine weiteren upstream Daten für die Eingabe verfügbar.  
  
## <a name="implementing-the-getdependentinputs-method"></a>Implementieren der GetDependentInputs-Methode  
 Wenn die benutzerdefinierte Datenflusskomponente mehr als zwei Eingaben unterstützt, müssen Sie auch eine Implementierung für die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse bereitstellen.  
  
> [!NOTE]  
>  Die Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode sollte nicht die Implementierungen in der Basisklasse aufrufen. Die Standardimplementierung dieser Methode in der Basisklasse löst lediglich eine `NotImplementedException` aus.  
  
 Die Datenfluss-Engine ruft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode nur auf, wenn der Benutzer mehr als zwei Eingaben an die Komponente anfügt. Wenn eine Komponente nur über zwei Eingaben verfügt und die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> -Methode gibt an, dass eine Eingabe blockiert ist (*CanProcess* = `false`), die Datenfluss-Engine weiß, dass die andere Eingabe auf den Empfang weiterer Daten wartet. Wenn jedoch mehr als zwei Eingaben vorhanden sind und die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode angibt, dass eine Eingabe blockiert ist, identifiziert der zusätzliche Code in <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>, welche Eingaben auf den Empfang weiterer Daten warten.  
  
> [!NOTE]  
>  Sie rufen die Methode <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> oder <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> nicht in eigenem Code auf. Die Datenfluss-Engine ruft diese Methoden und die anderen Methoden der `PipelineComponent`-Klasse auf, die Sie überschreiben, wenn die Datenfluss-Engine die Komponente ausführt.  
  
### <a name="example"></a>Beispiel  
 Wenn eine bestimmte Eingabe blockiert ist, gibt die folgende Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode eine Auflistung der Eingaben zurück, die auf den Empfang weiterer Daten warten und daher die betreffende Eingabe blockieren. Die Komponente identifiziert die blockierenden Eingaben, indem überprüft wird, ob außer der blockierten Eingabe andere Eingaben derzeit in den Puffern, die die Komponente bereits empfangen hat, nicht über Daten verfügen, die verarbeitet werden können (`inputBuffers[i].CurrentRow() == null`). Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode gibt dann die Auflistung der blockierenden Eingaben als Auflistung von Eingabe-IDs zurück.  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
