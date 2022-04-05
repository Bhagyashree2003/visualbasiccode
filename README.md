# visualbasiccode
Visual studio database code 

Imports System.Data.OleDb

Public Class Form1

    Dim conn As OleDbConnection = New OleDbConnection("Provider=Microsoft.ACE.OLEDB.12.0;Data Source=D:\VAIBHAVB\VB.NET\TestDB.accdb")
	
    Private Sub fetch()
        If conn.State = ConnectionState.Closed Then
            conn.Open()
        End If

        Try
            Dim cmd As OleDbCommand = New OleDbCommand("select * from Vaibhavb", conn)
            cmd.ExecuteScalar()

            Dim da As OleDbDataAdapter = New OleDbDataAdapter(cmd)
            Dim ds As DataSet = New DataSet

            da.Fill(ds)

            DataGridView1.DataSource = ds.Tables(0)
        Catch ex As Exception
            MessageBox.Show(ex.ToString())
        End Try

    End Sub

    Private Sub btnInsert_Click(sender As Object, e As EventArgs) Handles btnInsert.Click
        If conn.State = ConnectionState.Closed Then
            conn.Open()
        End If
        Try
            Dim cmd As OleDbCommand = New OleDbCommand("insert into Vaibhavb values(" & tbID.Text & " , '" & tbName.Text & "')", conn)
            cmd.ExecuteNonQuery()
        Catch ex As Exception
            MessageBox.Show(ex.ToString())
        End Try

        fetch()

    End Sub

    Private Sub btnUpdate_Click(sender As Object, e As EventArgs) Handles btnUpdate.Click

        If conn.State = ConnectionState.Closed Then
            conn.Open()
        End If

        Try
            Dim cmd As OleDbCommand = New OleDbCommand("update Vaibhavb set EmpName =  '" & tbName.Text & "' where ID = " & tbID.Text & "", conn)
            cmd.ExecuteNonQuery()
        Catch ex As Exception
            MessageBox.Show(ex.ToString())
        End Try
        fetch()

    End Sub

    Private Sub Delete_Click(sender As Object, e As EventArgs) Handles Delete.Click
        If conn.State = ConnectionState.Closed Then
            conn.Open()
        End If

        Try
            Dim cmd As OleDbCommand = New OleDbCommand("delete from Vaibhavb where ID = " & tbID.Text & "", conn)
            cmd.ExecuteNonQuery()
        Catch ex As Exception
            MessageBox.Show(ex.ToString())
        End Try
        fetch()

    End Sub

    Private Sub btnSearch_Click(sender As Object, e As EventArgs) Handles btnSearch.Click
        If conn.State = ConnectionState.Closed Then
            conn.Open()
        End If

        Try
            Dim dr As OleDbDataReader

            Dim cmd As OleDbCommand = New OleDbCommand("select * from Vaibhavb where ID = " & tbID.Text & "", conn)
            dr = cmd.ExecuteReader()

            dr.Read()

            tbName.Text = dr.Item(1)
            fetch()
        Catch ex As Exception
            MessageBox.Show(ex.ToString())
        End Try

    End Sub

    Private Sub btnShow_Click(sender As Object, e As EventArgs) Handles btnShow.Click
        fetch()
    End Sub


    Private Sub btnClear_Click(sender As Object, e As EventArgs) Handles btnClear.Click
        tbID.Clear()
        tbName.Clear()
    End Sub

End Class
