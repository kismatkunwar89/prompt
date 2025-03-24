Usecase1

Test 1
During a digital forensics investigation, among many prefetch files , two suspicious Prefetch files were discovered in C:\Windows\Prefetch\

Artifact 1: Prefetch 
  - Source: C:\Windows\Prefetch\
  - File Name: CCSETUP.EXE-8F9E1A2B.pf
  - Process Executable: ccsetup.exe
  - Process Path: C:\Users\Public\Downloads\ccsetup.exe

Artifact 2: Prefetch
  - Source: C:\Windows\Prefetch\
  - File Name: TEAMVIEWER_SETUP.EXE-4A1B2C3D.pf
  - Process Executable: TeamViewer_Setup.exe
  - Process Path: C:\Users\Public\Downloads\TeamViewer_Setup.exe

Test 2

During an investigation while looking for ccsetup.exe the following files were found in the directory C:\Users\Public\Downloads\ but not ccsetup.exe
- TeamViewer_Setup.exe
- chrome_installer.exe
- 7z2301.exe
- readme.txt
- report.pdf


Test 3

During a digital forensics investigation, among many Prefetch files, two suspicious Prefetch artifacts were discovered in C:\Windows\Prefetch\:

Artifact 1: Prefetch  
  - Source: C:\Windows\Prefetch\  
  - File Name: CCSETUP.EXE-8F9E1A2B.pf  which had properties Process Executable: ccsetup.exe  and Process Path: C:\Users\Public\Downloads\ccsetup.exe  

Artifact 2: Prefetch  
  - Source: C:\Windows\Prefetch\  
  - File Name: TEAMVIEWER_SETUP.EXE-4A1B2C3D.pf  which had properties Process Executable: TeamViewer_Setup.exe  and Process Path: C:\Users\Public\Downloads\TeamViewer_Setup.exe  

After analyzing prefetch files ,  the directory C:\Users\Public\Downloads\ was examined. The only following files were present in the folder:
- TeamViewer_Setup.exe
- chrome_installer.exe
- 7z2301.exe
- readme.txt
- report.pdf

The file ccsetup.exe was **not found** in this directory or anywhere else on the system.


Use Case 2

During a forensic investigation of a Windows NTFS system, the Master File Table (C:\$MFT) was parsed. Investigators extracted several file records linked to the user profile `C:\Users\Alice\`.

Multiple `.lnk` shortcut files and their associated targets were identified across distinct MFT records. Most shortcut relationships were timestamp-consistent. However, one `.lnk` file referencing `password.docx` was created **before** the target file existed, suggesting a possible anti-forensics artifact.


Test 1 : only one artifact as all are from same mft record , Test 2 : for all related artifacts together

Below are the artifacts from the parsed MFT:

Artifact 1: password.docx  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116327  
- File Name: password.docx  
- Path: C:\Users\Alice\Documents\password.docx  
- Extension: .docx  
- Creation Time (NTFS 0x10): 2025-03-04T10:15:00Z  

Artifact 2: password.lnk  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116328  
- File Name: password.lnk  
- Path: C:\Users\Alice\AppData\Roaming\Microsoft\Windows\Recent\password.lnk  
- Extension: .lnk  
- Creation Time (NTFS 0x10): 2025-03-04T01:10:00Z  
- Local Base Path (parsed from LNK metadata): C:\Users\Alice\Documents\password.docx  

Test 2: All together

Artifact 3: budget.xlsx  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116329  
- File Name: budget.xlsx  
- Path: C:\Users\Alice\Documents\budget.xlsx  
- Extension: .xlsx  
- Creation Time (NTFS 0x10): 2025-03-01T13:00:00Z  

Artifact 4: budget.lnk  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116330  
- File Name: budget.lnk  
- Path: C:\Users\Alice\AppData\Roaming\Microsoft\Windows\Recent\budget.lnk  
- Extension: .lnk  
- Creation Time (NTFS 0x10): 2025-03-01T13:15:00Z  
- Local Base Path (parsed from LNK metadata): C:\Users\Alice\Documents\budget.xlsx  

Artifact 5: confidential.txt  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116331  
- File Name: confidential.txt  
- Path: C:\Users\Alice\Desktop\confidential.txt  
- Extension: .txt  
- Creation Time (NTFS 0x10): 2025-03-02T09:00:00Z  

Artifact 6: confidential.lnk  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116332  
- File Name: confidential.lnk  
- Path: C:\Users\Alice\AppData\Roaming\Microsoft\Windows\Recent\confidential.lnk  
- Extension: .lnk  
- Creation Time (NTFS 0x10): 2025-03-02T09:10:00Z  
- Local Base Path (parsed from LNK metadata): C:\Users\Alice\Desktop\confidential.txt  


Use case 3 

During a digital forensics investigation of a Windows system, inconsistencies were identified suggesting the deletion of a user profile. A successful interactive logon was recorded for the username john.doe and the user was still present in the system's registry account list.
, but no corresponding user profile folder existed (suspected to have been deleted).

---
Test 1
Artifact 1: Windows Security Event Log  with event id 4624
- **Source**: `C:\Windows\System32\winevt\Logs\Security.evtx`  
- **Type**: Windows Event Log  
- **Event Records**:  from source `C:\Windows\System32\winevt\Logs\Security.evtx`  
  - **Event ID**: 4624 — Account Name: `administrator` — Logon Type: 2  
  - **Event ID**: 4624 — Account Name: `john.doe` — Logon Type: 2  
  - **Event ID**: 4624 — Account Name: `user1` — Logon Type: 3  

---
Test2

Artifact 2: SAM Registry Hive (Local Accounts)  
- **Source**: `HKEY_LOCAL_MACHINE\SAM\Domains\Account\Users\Names`  
- **Type**: Windows Registry Hive  
- **Observed Subkeys (Usernames)**:  
  - `administrator`  
  - `user1`  
  - `johndoe`  
  
 Test3

✅ Artifact 3: User Profile Directory Listing  
- **Source**: `C:\Users\`  
- **Type**: File System Directory  
- **User Folders Present**:  
  - `C:\Users\administrator`  
  - `C:\Users\user1`  
  - `C:\Users\public`  
- **No folder found for**: `john.doe`


Case4

During a digital forensics investigation, an investigator identified potential system timestamp manipulation on a Windows system. The USNJRNL (Update Sequence Number Journal) was analyzed, and the following artifacts  were extracted were suspicious

Artifact 1: USN Record 
Update Sequence Number (USN): 287563224
Timestamp: 2025-02-18T10:15:00
Update Reason: FileCreate
Artifact 2: USN Record
Update Sequence Number (USN): 287563230 
Timestamp: 2025-02-14T10:16:00
Update Reason: FileModify




