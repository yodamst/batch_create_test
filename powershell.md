_PowerShellは、Microsoftが提供するタスク自動化および構成管理のフレームワークで、_
_コマンドラインシェルと関連するスクリプト言語で構成されている。_
_これは、.NETフレームワーク上に構築されており、Windowsシステムの管理や自動化に強力なツールである。_


*PowerShellの概要*
```
・コマンドレット (Cmdlets): PowerShellのコマンドは「コマンドレット」と呼ばれます。各コマンドレットは軽量のコマンドで、PowerShell環境で使用されます。
・オブジェクト: PowerShellはテキストではなくオブジェクトを扱います。コマンドレットはオブジェクトを出力し、これをパイプラインを通じて他のコマンドレットに渡すことができます。
・パイプライン: PowerShellではパイプライン（|）を使用して、あるコマンドレットの出力を他のコマンドレットの入力として渡すことができます。
```


*基本コマンド*

Get-Command
```
説明: 使用可能なコマンドレット、関数、ワークフロー、エイリアスを一覧表示します。
使用法: Get-Command
```


Get-Help
```
説明: コマンドレットや概念についてのヘルプを提供します。
使用法: Get-Help Get-Command（Get-Commandコマンドレットのヘルプを表示）
ヒント: -Onlineを使用すると、Webブラウザでヘルプトピックを表示できます。また、-Examplesで使用例を見ることができます。
```


Get-Service
```
説明: ローカルまたはリモートマシン上のサービスの状態を取得します。
使用法: Get-Service
```


Get-Process
```
説明: ローカルまたはリモートマシン上で実行中のプロセスを取得します。
使用法: Get-Process
```


Set-ExecutionPolicy
```
説明: PowerShellスクリプト実行ポリシーのユーザー設定を変更します。
使用法: Set-ExecutionPolicy RemoteSigned（ローカルスクリプトおよび信頼された発行者によって署名されたスクリプトを許可）
```


Get-Item
```
説明: 指定された場所のアイテムを取得します。
使用法: Get-Item -Path "C:\Windows\System32"
```


Set-Item
```
説明: アイテムの値を指定された値に変更します。
使用法: Set-Item -Path "HKLM:\Software\MyCompany\MyApp" -Value "MyValue"
```


New-Item
```
説明: 新しいアイテムを作成します。
使用法: New-Item -Path "C:\Temp\NewFolder" -ItemType Directory
```


Remove-Item
```
説明: 指定されたアイテムを削除します。
使用法: Remove-Item -Path "C:\Temp\OldFile.txt"
```


Copy-Item
```
説明: アイテムをある場所から別の場所にコピーします。
使用法: Copy-Item -Path "C:\Temp\OldFile.txt" -Destination "C:\Temp\NewFile.txt"
```


Move-Item
```
説明: アイテムをある場所から別の場所に移動します。
使用法: Move-Item -Path "C:\Temp\OldFile.txt" -Destination "C:\Temp\NewFolder\"
```

使用例
```
Get-Service

Get-Help Get-Service

Start-Service -Name "wuauserv"

Stop-Service -Name "wuauserv"

Get-Process

Copy-Item -Path "C:\example\file.txt" -Destination "C:\example\backup\file.txt"
```




*出力テスト.ps1*
```
Write-Output "出力テスト"
```


*BackupScript.ps1*
```
# バックアップ元と先のパスを指定
$sourcePath = "バックアップ元"
$backupPath = "バックアップ先"

# バックアップ先のフォルダが存在しない場合は作成
if (-Not (Test-Path -Path $backupPath)) {
    New-Item -ItemType Directory -Path $backupPath
}

# フォルダの内容をコピー
Copy-Item -Path $sourcePath\* -Destination $backupPath -Recurse

Write-Output "Backup completed successfully."
```


*スケジュールの作成*
```
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "実行したいps1"
$trigger = New-ScheduledTaskTrigger -Daily -At 5AM
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "DailyBackup" -Description "Daily backup of important files"
```

*日*
```
$trigger = New-ScheduledTaskTrigger -Daily -At 5AM

・-Daily: 毎日指定した時間に実行。
・-At: 実行する時間を指定。
```

*週*
```
$trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek Monday,Wednesday,Friday -At 3AM
・-Weekly: 毎週指定した曜日に実行。
・-DaysOfWeek: 実行する曜日を指定。複数の曜日を指定する場合はカンマで区切ります。
・-At: 実行する時間を指定。
```

*Weeklyの詳細*
```
$trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek Monday,Wednesday,Friday -At 3AM -WeeksInterval 2
・-WeeksInterval: タスクが実行される週の間隔を指定。例では、2週間ごとに実行。
```

*月*
```
$trigger = New-ScheduledTaskTrigger -Monthly -DaysOfMonth 1,15 -At 3AM
・-Monthly: 毎月指定した日に実行します。
・-DaysOfMonth: 実行する日を指定します。複数の日を指定する場合はカンマで区切ります。
・-At: 実行する時間を指定します。
```

*Monthlyの詳細オプション*
```
$trigger = New-ScheduledTaskTrigger -Monthly -DaysOfMonth 1,15 -At 3AM -MonthsOfYear January,June,December
・-MonthsOfYear: タスクが実行される月を指定します。この例では、1月、6月、12月に実行。
```

*MonthlyDOW（指定された月の曜日）*
```
$trigger = New-ScheduledTaskTrigger -MonthlyDOW -WeeksOfMonth First,Third -DaysOfWeek Monday,Wednesday -MonthsOfYear January,June,December -At 3AM
・-MonthlyDOW: 指定された月の特定の曜日にタスクを実行します。
・-WeeksOfMonth: 月の第何週に実行するかを指定します（First, Second, Third, Fourth, Last）。
・-DaysOfWeek: 実行する曜日を指定します。
・-MonthsOfYear: タスクが実行される月を指定します。
```

*Once（一回）*
```
-Once: 一度だけ実行。
-At: 実行する日時を指定。日時はISO 8601形式（YYYY-MM-DDTHH:MM
）で指定。
```

*応用編*
```
$trigger = New-ScheduledTaskTrigger -MonthlyDOW -WeeksOfMonth First,Third -DaysOfWeek Monday,Wednesday -MonthsOfYear January,June,December -At 3AM
```

