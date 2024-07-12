_PowerShell�́AMicrosoft���񋟂���^�X�N����������э\���Ǘ��̃t���[�����[�N�ŁA_
_�R�}���h���C���V�F���Ɗ֘A����X�N���v�g����ō\������Ă���B_
_����́A.NET�t���[�����[�N��ɍ\�z����Ă���AWindows�V�X�e���̊Ǘ��⎩�����ɋ��͂ȃc�[���ł���B_


*PowerShell�̊T�v*
```
�E�R�}���h���b�g (Cmdlets): PowerShell�̃R�}���h�́u�R�}���h���b�g�v�ƌĂ΂�܂��B�e�R�}���h���b�g�͌y�ʂ̃R�}���h�ŁAPowerShell���Ŏg�p����܂��B
�E�I�u�W�F�N�g: PowerShell�̓e�L�X�g�ł͂Ȃ��I�u�W�F�N�g�������܂��B�R�}���h���b�g�̓I�u�W�F�N�g���o�͂��A������p�C�v���C����ʂ��đ��̃R�}���h���b�g�ɓn�����Ƃ��ł��܂��B
�E�p�C�v���C��: PowerShell�ł̓p�C�v���C���i|�j���g�p���āA����R�}���h���b�g�̏o�͂𑼂̃R�}���h���b�g�̓��͂Ƃ��ēn�����Ƃ��ł��܂��B
```


*��{�R�}���h*

Get-Command
```
����: �g�p�\�ȃR�}���h���b�g�A�֐��A���[�N�t���[�A�G�C���A�X���ꗗ�\�����܂��B
�g�p�@: Get-Command
```


Get-Help
```
����: �R�}���h���b�g��T�O�ɂ��Ẵw���v��񋟂��܂��B
�g�p�@: Get-Help Get-Command�iGet-Command�R�}���h���b�g�̃w���v��\���j
�q���g: -Online���g�p����ƁAWeb�u���E�U�Ńw���v�g�s�b�N��\���ł��܂��B�܂��A-Examples�Ŏg�p������邱�Ƃ��ł��܂��B
```


Get-Service
```
����: ���[�J���܂��̓����[�g�}�V����̃T�[�r�X�̏�Ԃ��擾���܂��B
�g�p�@: Get-Service
```


Get-Process
```
����: ���[�J���܂��̓����[�g�}�V����Ŏ��s���̃v���Z�X���擾���܂��B
�g�p�@: Get-Process
```


Set-ExecutionPolicy
```
����: PowerShell�X�N���v�g���s�|���V�[�̃��[�U�[�ݒ��ύX���܂��B
�g�p�@: Set-ExecutionPolicy RemoteSigned�i���[�J���X�N���v�g����ѐM�����ꂽ���s�҂ɂ���ď������ꂽ�X�N���v�g�����j
```


Get-Item
```
����: �w�肳�ꂽ�ꏊ�̃A�C�e�����擾���܂��B
�g�p�@: Get-Item -Path "C:\Windows\System32"
```


Set-Item
```
����: �A�C�e���̒l���w�肳�ꂽ�l�ɕύX���܂��B
�g�p�@: Set-Item -Path "HKLM:\Software\MyCompany\MyApp" -Value "MyValue"
```


New-Item
```
����: �V�����A�C�e�����쐬���܂��B
�g�p�@: New-Item -Path "C:\Temp\NewFolder" -ItemType Directory
```


Remove-Item
```
����: �w�肳�ꂽ�A�C�e�����폜���܂��B
�g�p�@: Remove-Item -Path "C:\Temp\OldFile.txt"
```


Copy-Item
```
����: �A�C�e��������ꏊ����ʂ̏ꏊ�ɃR�s�[���܂��B
�g�p�@: Copy-Item -Path "C:\Temp\OldFile.txt" -Destination "C:\Temp\NewFile.txt"
```


Move-Item
```
����: �A�C�e��������ꏊ����ʂ̏ꏊ�Ɉړ����܂��B
�g�p�@: Move-Item -Path "C:\Temp\OldFile.txt" -Destination "C:\Temp\NewFolder\"
```

�g�p��
```
Get-Service

Get-Help Get-Service

Start-Service -Name "wuauserv"

Stop-Service -Name "wuauserv"

Get-Process

Copy-Item -Path "C:\example\file.txt" -Destination "C:\example\backup\file.txt"
```




*�o�̓e�X�g.ps1*
```
Write-Output "�o�̓e�X�g"
```


*BackupScript.ps1*
```
# �o�b�N�A�b�v���Ɛ�̃p�X���w��
$sourcePath = "�o�b�N�A�b�v��"
$backupPath = "�o�b�N�A�b�v��"

# �o�b�N�A�b�v��̃t�H���_�����݂��Ȃ��ꍇ�͍쐬
if (-Not (Test-Path -Path $backupPath)) {
    New-Item -ItemType Directory -Path $backupPath
}

# �t�H���_�̓��e���R�s�[
Copy-Item -Path $sourcePath\* -Destination $backupPath -Recurse

Write-Output "Backup completed successfully."
```


*�X�P�W���[���̍쐬*
```
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "���s������ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At 5AM
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "DailyBackup" -Description "Daily backup of important files"
```

*��*
```
$trigger = New-ScheduledTaskTrigger -Daily -At 5AM

�E-Daily: �����w�肵�����ԂɎ��s�B
�E-At: ���s���鎞�Ԃ��w��B
```

*�T*
```
$trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek Monday,Wednesday,Friday -At 3AM
�E-Weekly: ���T�w�肵���j���Ɏ��s�B
�E-DaysOfWeek: ���s����j�����w��B�����̗j�����w�肷��ꍇ�̓J���}�ŋ�؂�܂��B
�E-At: ���s���鎞�Ԃ��w��B
```

*Weekly�̏ڍ�*
```
$trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek Monday,Wednesday,Friday -At 3AM -WeeksInterval 2
�E-WeeksInterval: �^�X�N�����s�����T�̊Ԋu���w��B��ł́A2�T�Ԃ��ƂɎ��s�B
```

*��*
```
$trigger = New-ScheduledTaskTrigger -Monthly -DaysOfMonth 1,15 -At 3AM
�E-Monthly: �����w�肵�����Ɏ��s���܂��B
�E-DaysOfMonth: ���s��������w�肵�܂��B�����̓����w�肷��ꍇ�̓J���}�ŋ�؂�܂��B
�E-At: ���s���鎞�Ԃ��w�肵�܂��B
```

*Monthly�̏ڍ׃I�v�V����*
```
$trigger = New-ScheduledTaskTrigger -Monthly -DaysOfMonth 1,15 -At 3AM -MonthsOfYear January,June,December
�E-MonthsOfYear: �^�X�N�����s����錎���w�肵�܂��B���̗�ł́A1���A6���A12���Ɏ��s�B
```

*MonthlyDOW�i�w�肳�ꂽ���̗j���j*
```
$trigger = New-ScheduledTaskTrigger -MonthlyDOW -WeeksOfMonth First,Third -DaysOfWeek Monday,Wednesday -MonthsOfYear January,June,December -At 3AM
�E-MonthlyDOW: �w�肳�ꂽ���̓���̗j���Ƀ^�X�N�����s���܂��B
�E-WeeksOfMonth: ���̑扽�T�Ɏ��s���邩���w�肵�܂��iFirst, Second, Third, Fourth, Last�j�B
�E-DaysOfWeek: ���s����j�����w�肵�܂��B
�E-MonthsOfYear: �^�X�N�����s����錎���w�肵�܂��B
```

*Once�i���j*
```
-Once: ��x�������s�B
-At: ���s����������w��B������ISO 8601�`���iYYYY-MM-DDTHH:MM
�j�Ŏw��B
```

*���p��*
```
$trigger = New-ScheduledTaskTrigger -MonthlyDOW -WeeksOfMonth First,Third -DaysOfWeek Monday,Wednesday -MonthsOfYear January,June,December -At 3AM
```

