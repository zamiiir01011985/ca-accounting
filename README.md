# accounting
CA-Accounting
Public Class SalaryCalculator
    Private Sub btnCalculate_Click(sender As Object, e As EventArgs) Handles btnCalculate.Click
        ' Get input values
        Dim basicSalary As Decimal
        Dim hoursWorked As Decimal
        Dim overtimeHours As Decimal
        
        ' Validate inputs
        If Not Decimal.TryParse(txtBasicSalary.Text, basicSalary) Then
            MessageBox.Show("Please enter a valid basic salary", "Input Error")
            Return
        End If
        
        If Not Decimal.TryParse(txtHoursWorked.Text, hoursWorked) Then
            hoursWorked = 0
        End If
        
        If Not Decimal.TryParse(txtOvertimeHours.Text, overtimeHours) Then
            overtimeHours = 0
        End If
        
        ' Calculate allowances
        Dim housingAllowance As Decimal = basicSalary * 0.2 ' 20% of basic
        Dim transportAllowance As Decimal = basicSalary * 0.1 ' 10% of basic
        Dim overtimePay As Decimal = (basicSalary / 160) * 1.5 * overtimeHours ' 1.5x hourly rate
        
        ' Calculate gross salary
        Dim grossSalary As Decimal = basicSalary + housingAllowance + transportAllowance + overtimePay
        
        ' Calculate deductions
        Dim taxRate As Decimal = 0.15 ' 15% tax
        Dim tax As Decimal = grossSalary * taxRate
        Dim pensionContribution As Decimal = basicSalary * 0.08 ' 8% pension
        Dim healthInsurance As Decimal = 500 ' Fixed amount
        
        ' Calculate total deductions
        Dim totalDeductions As Decimal = tax + pensionContribution + healthInsurance
        
        ' Calculate net salary
        Dim netSalary As Decimal = grossSalary - totalDeductions
        
        ' Display results
        txtHousingAllowance.Text = housingAllowance.ToString("N2")
        txtTransportAllowance.Text = transportAllowance.ToString("N2")
        txtOvertimePay.Text = overtimePay.ToString("N2")
        txtGrossSalary.Text = grossSalary.ToString("N2")
        txtTax.Text = tax.ToString("N2")
        txtPension.Text = pensionContribution.ToString("N2")
        txtHealthInsurance.Text = healthInsurance.ToString("N2")
        txtTotalDeductions.Text = totalDeductions.ToString("N2")
        txtNetSalary.Text = netSalary.ToString("N2")
        
        ' Update summary label
        lblSummary.Text = $"Worker receives a net salary of {netSalary:C} after deductions"
    End Sub
    
    Private Sub btnClear_Click(sender As Object, e As EventArgs) Handles btnClear.Click
        ' Clear all input fields
        txtBasicSalary.Clear()
        txtHoursWorked.Clear()
        txtOvertimeHours.Clear()
        
        ' Clear all output fields
        txtHousingAllowance.Clear()
        txtTransportAllowance.Clear()
        txtOvertimePay.Clear()
        txtGrossSalary.Clear()
        txtTax.Clear()
        txtPension.Clear()
        txtHealthInsurance.Clear()
        txtTotalDeductions.Clear()
        txtNetSalary.Clear()
        lblSummary.Text = ""
        
        ' Set focus to first field
        txtBasicSalary.Focus()
    End Sub
    
    Private Sub btnExit_Click(sender As Object, e As EventArgs) Handles btnExit.Click
        Me.Close()
    End Sub
    
    ' Function to calculate salary (can be called from other forms)
    Public Function CalculateWorkerSalary(basic As Decimal, overtime As Decimal) As Decimal
        Dim housing As Decimal = basic * 0.2
        Dim transport As Decimal = basic * 0.1
        Dim overtimePay As Decimal = (basic / 160) * 1.5 * overtime
        Dim gross As Decimal = basic + housing + transport + overtimePay
        Dim tax As Decimal = gross * 0.15
        Dim pension As Decimal = basic * 0.08
        Dim health As Decimal = 500
        Dim net As Decimal = gross - tax - pension - health
        Return net
    End Function
End Class
