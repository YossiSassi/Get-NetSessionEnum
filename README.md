.SYNOPSIS

This script automates the enumeration of NetSessionEnum (network sessions of connected users in the domain), providing an easy and object-based output to facilitate AD Reconnaissance for Adversary simulation & Red Teams.

.DESCRIPTION

This script will enumerate net connections to specific computers and users, or by default, to all domain controllers by all domain users, and output the username, the IP he's logged on from, the hostname he's logged on from, to which computer/Domain Controller he's connected to, how long he's connected to this computer, and how long has he been idle (or, effectively, when he was last active on that connection).
It uses the NetSess tool by Joe Richards, yet only as Bytes, so effectively, all you need is this script with no other dependencies. It can output the reconnaissance data to the screen, as an unfiltered object (that you can query and filter as Cached Results for fast performance), or to a GUI (using PowerShell ISE).

.PARAMETER UserName

The UserName to filter the results by. Default is all Domain users.

.PARAMETER ComputerName

The ConnectedTo computer name, to filter the results by. Default is all Domain Controllers.

.PARAMETER UseCachedResults

Makes subsequent runs of the script perform much faster, using Cached results from previous run.
Highly useful when you want to query other users or open as gui *after* the initial run.

.PARAMETER AllDomainComputers

Checks for connected users on all computer account in the domain. Cannot be used together with -ComputerName (will override -ComputerName when used at the same run).

.PARAMETER OpenAsGUI

Opens the results in a GUI form. Requires PowerShell ISE to be installed on this machine.

.EXAMPLE

Get-NetSessionEnum

Runs the initial & full scan with default choices - all users on all domain cotrollers. Recommended if you need a full scan, or if want to run the script again with other/more parameters and filters later.

.EXAMPLE

Get-NetSessionEnum -UserName administrator

Brings all the network connections made by the user with SamAccountName administrator. Invokes a full (fresh) scan on all domain computers.

.EXAMPLE

Get-NetSessionEnum -AllDomainComputers

Invokes a full scan for all connected users on all domain computers. Note that this takes longer to complete, yet useful if you want query for user connections across all domain clients.

.EXAMPLE

Get-NetSessionEnum -UserName administrator -ComputerName WIN7-PC, WIN10-PC, DC2

Brings all the network connections made by the user with SamAccountName administrator to those 3 specified computers.

.EXAMPLE

Get-NetSessionEnum -UseCachedResults -UserName administrator
Brings all the network connections made by the user with SamAccountName administrator from previously cached results (meaning, the script must have ran at least once before). Gives MUCH faster performance, as the previous scan results are already in memory and just filtered but username.

.EXAMPLE

Get-NetSessionEnum -OpenAsGUI

Runs a full 'fresh' scan with default choices (all users on all domain controllers) and outputs the results into an adhoc GUI (form), that you can easily filter by typing in your keywords (username, computer..) or using specific criterias, directly on the form.

.NOTES

v1.0 by Y1nTh35h3ll. Comments welcome to yossis@protonmail.com. Special Thanks to Joe Richards (joe@joeware.net) for his NetSess tool.

.LINK

https://www.CyberArtSecurity.com
