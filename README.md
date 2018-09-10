# Activesync-Device-report
Creating activesync device reports for Office 365 using powershell

# Exchange Online Device partnership inventory
#  EXO_MobileDevice_Inventory.ps1
#  
#  Created by: Austin McCollum 2/11/2018 austinmc@microsoft.com
#  Updated by: Garrin Thompson 3/2/2018 garrint@microsoft.com *** "Borrowed" a few quality-of-life functions from Start-RobustCloudCommand.ps1
#
#########################################################################################
# This script enumerates all devices in Office 365 and reports on many properties of the
#   device/application and the mailbox owner.
#
# $deviceList is an array of hashtables, because deviceIDs may not be
#   unique in an environment. For instance when a device is configured with
#   two separate mailboxes in the same org, the same deviceID will appear twice.
#   Hashtables require uniqueness of the key so that's why the array of hashtable data 
#   structure was chosen.
#
# The devices can be sorted by a variety of properties like "LastActivity" to determine 
#   stale partnerships or outdated devices needing to be removed.
# 
# The DisplayName of the user's CAS mailbox is recorded for importing with the 
#   Set-CasMailbox commandlet to configure allowedDeviceIDs. This is especially useful in 
#   scenarios where a migration to ABQ framework requires "grandfathering" in all or some
#   of the existing partnerships.
#
# Get-CasMailbox is run efficiently with the -HasActiveSyncDevicePartnership filter 
#########################################################################################
