New-Item -Type File -Path .\report.csv
$headers = "Username, PwLastSet"
Set-Content -Path .\report.csv -Value $headers

$expired_accounts_list = Get-ADUser -Filter * -Properties Name, PasswordNeverExpires | Where-Object { $_.PasswordNeverExpires -eq "True" } | Where-Object {$_.Enabled -eq "True"}
foreach ($account in $expired_accounts_list){
    $username = $account.SamAccountName
    try {
        $pw_last_set = Get-ADUser $username -Prop PasswordLastSet | Select-Object -ExpandProperty PasswordLastSet
        $pw_last_set_date = $pw_last_set.ToString("MM/dd/yyyy")
        $row = "$username, $pw_last_set_date"
        Add-Content -Path .\report.csv -Value $row
    }
    Catch {
        $row2 = "$username, Error Fetching Account Details" 
        Add-Content -Path .\report.csv -Value $row
    }
   
    
}
