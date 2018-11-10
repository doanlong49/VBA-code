# VBA-code
Sub Cau1()
Dim Dic1 As Object, iRow As Long, i As Long
Dim Arr() As Variant, TmpArr As Variant
With Sheets("Cau1")
 .Range("E4:H10").ClearContents
  Set Dic1 = CreateObject("Scripting.Dictionary")
    TmpArr = Sheet1.Range("b2:g21").Value
    ReDim Arr(1 To UBound(TmpArr, 1), 1 To 6)
    For iRow = 1 To UBound(TmpArr, 1)
        If Not IsEmpty(TmpArr(iRow, 2)) And Not Dic1.exists(TmpArr(iRow, 2)) Then
            i = i + 1
             Dic1.Add TmpArr(iRow, 2), i
             Arr(i, 1) = TmpArr(iRow, 1)
             Arr(i, 2) = TmpArr(iRow, 2)
            If TmpArr(iRow, 3) <> "" Then
                Arr(i, 3) = TmpArr(iRow, 6)
            Else
                Arr(i, 4) = TmpArr(iRow, 6)
            End If
        Else
            If TmpArr(iRow, 3) <> "" Then
                Arr(Dic1.Item(TmpArr(iRow, 2)), 3) = Arr(Dic1.Item(TmpArr(iRow, 2)), 3) + TmpArr(iRow, 6)
            Else
                
             Arr(Dic1.Item(TmpArr(iRow, 2)), 4) = Arr(Dic1.Item(TmpArr(iRow, 2)), 4) + TmpArr(iRow, 6)
                
            End If
        End If
    Next iRow
.Range("e4").Resize(i, 4).Value = Arr
End With
End Sub
