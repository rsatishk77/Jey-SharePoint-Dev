Function CheckForm()
CheckForm=True
	If Len(Trim(document.frm.txtComments.value)) > 0 Then
		document.frm.AddComment.value = "Yes"
		document.frm.action="test.asp"
	Else
		If frm.txtPrev.value = "NO" then
			Alert "You have not entered a comment"
			CheckForm=False
		End if
	End if		
End Function

-------------------------------------------------------------------

Dim value1
value1= CStr(CCur(value1)) 

-------------------------------------------------------------------
Dim value
value = "abc12344345" 
select case Mode

	case "1"		
		Value = Replace(value, ".", "")
		If Len(value) >= 2 And IsNumeric(value) Then
			call test1
		End If
	case "2"
		Value = Replace(value, ".", "")
		If Len(value) >= 4 And IsNumeric(value) Then
			call test2
		End If
	case "3"
		If IsNumeric(value) Then
			PassValue = Right("00000000" & value, 9)		
			call test3
		ElseIf Len(Trim(value)) = 0 Then			
			value = "000000000"			
			call test3
		End If
	case "4"
		PassValue = Right("00000" & value, 5)		
		call test4
end select 

-------------------------------------------------------------------
Function ValidateForm()

	ValidateForm = True

	If Len(Trim(document.frm.txtAmount.value)) > 0 Then
		strAmount = Trim(document.frm.txtAmount.value)

		'make sure it is numeric				
		If Not IsNumeric(strAmount) Then
			document.frm.action = "create.asp"
			document.frm.txtError.value = "Yes"
			Exit Function
		Else
			'If the user entered a decimal point.
			strAmount = CStr(CCur(strAmount))
			intDecimalLocation = InStr(1, strAmount, ".")
			If intDecimalLocation > 0 Then
				If (Len(strAmount) - intDecimalLocation) > 2 Then
					document.frm.action = "create.asp"
					document.frm.txtError.value = "Yes"
					Exit Function
				Else
					'add extra zeros to make 2 places after the decimal point.
					If (Len(strAmount) - intDecimalLocation) = 1 Then
						strAmount = strAmount + "0"
						document.frm.txtAmount.value = strAmount
					End if						

					'error if negative							
					If CCur(strAmount) <= 0 Then
						document.frm.action = "create.asp"
						document.frm.txtError.value = "Yes"
						Exit Function
					End If
				End If
			Else
				'error if negative							
				If CCur(strAmount) <= 0 Then
					document.frm.action = "create.asp"
					document.frm.txtError.value = "Yes"
					Exit Function
				End If
			End If					
		End If		
	End If
End Function
