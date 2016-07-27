Function DriveClean{
# Root(r, string), Author(auth, string)
Param ([Parameter(Mandatory=$True)][string]$r, [Parameter(Mandatory=$False)][string]$auth)

Process{
    Get-ChildItem $r -Recurse -File | ForEach-Object{
    $att = @{Path = $_.FullName; SizeMB = $_.Length / 1MB; Author = (Get-Acl $_.FullName).Owner; Modified = $_.LastWriteTime; LastAccesTime = $_.LastAccessTime; CreationTime = $_.CreationTime }

    New-Object PSObject -Property $att
    } | Select-Object Path, SizeMB, CreationTime, Modified, LastAccesTime, Author | Sort SizeMB -Descending | Select -First 10 | Where-Object Author -Match $auth | 
        Export-CSV -encoding Unicode -Path "\\hpnode1\ict\ICTTeams\User Support\DriveCleanup\DriveClean.csv" -Delimiter ";"
    }
}

DriveClean -r "\\hpnode1\ict\ICTTeams\User Support\SIP" -auth "domain\username"
