Public Class Form1
    ''funcion que valida para que el cuadro de texto solo se pueda ingresar numeros
    Private Sub VALIDAR(ByRef E As System.Windows.Forms.KeyPressEventArgs)
        If Char.IsDigit(E.KeyChar) Then
            E.Handled = False

        ElseIf Char.IsControl(E.KeyChar) Then
            E.Handled = False

        Else
            E.Handled = True
        End If
    End Sub
    ''llamamos el evento del cuadro de texo a keypress donde llamamos la funcion de validar
    Private Sub txtnumero_KeyPress(sender As Object, e As KeyPressEventArgs) Handles txtnumero.KeyPress
        VALIDAR(e)
    End Sub

    Private Sub btncalcular_Click(sender As Object, e As EventArgs) Handles btncalcular.Click
        Dim n1(15), suma(15), vector(15), resultado As Integer
        Dim n(15), cadena As String
        cadena = txtnumero.Text
        For i = 0 To 15 Step 1
            n(i) = cadena.Substring(i, 1)
            n1(i) = Convert.ToInt16(n(i))
        Next
        For j = 15 To 0 Step -1
            If j Mod 2 = 0 Then
                vector(j) = n1(j) * 2
            Else
                vector(j) = n1(j)
            End If
            If vector(j) >= 10 Then
                suma(j) = ((vector(j) Mod 10) + (vector(j) \ 10))
            Else
                suma(j) = vector(j)
            End If

            resultado = resultado + suma(j)


        Next
        If resultado Mod 10 = 0 Then
            MsgBox(" El numero de su tarjetaes correcto ")
        Else
            MsgBox(" El numero de su tarjeta " + cadena.ToString + " es invalido", MsgBoxStyle.Critical, "Verificacion de número de targeta")
        End If
    End Sub
End Class
