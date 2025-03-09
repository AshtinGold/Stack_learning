Here are solutions to common conda and jupyter notebook problems and various helpful tricks to help speed up your coding!  
  
## Issue 1:
`& was unexpected at this time. The value specified in an AutoRun registry key could not be parsed.`

Happened to me after installing miniconda on WIN11. The solution is to run:
`conda init powershell`
