	
		1.RegistryChangesView (before everything)
			Create snapshots, differencial analysis
		2. ProcMon
			Ability to apply filters
		3. FileActi ityView
		4. Volatility,. Pslist
		5. Ftk imager
		6. Autopsy
		7. PeStudio (before running malware, open malware.exe in pestudio)
			Get executable properties, Get imported functions
	
	Before everything:
		Open RegistryChangeView
		Registry Data Source 1: Saved Registry Snapshot
		Create Registry Snapshot
		OK
		Quit

	1. Take image of partition using FTK Imager:

					File > Create Disk Image:
								Select Source Window:
										Physical Drive
										Next
								Select Drive:
									"1gb olan drive" 
									Finish
								Create Image Window:
									Click Add:
										Select Image Type - E01 > Next

					Evidence Item Information:
							Case Number: Case001
							Evidence Number: Evidence001
							Unique Description: Digital Forensics Final Exam
							Examiner: John Kohn

					Select Image destination Window:
									Image Destination Folder: Z:\
									Image Filename: Disk_X_Image
									Finish
			

		!!!! PIN CMD TO TASKBAR
		
		2. Run the malicious executable:

					Double-Click X:\malwex.cmd
		3. Restart VM
			In Cmd :
				cd C:\4n6\FTK Imager 
				"FTK Imager.exe"
				
		4. Capture the Memory using FTK Imager

					File > Capture Memory:
							Destination path: Z:\
							Destination filename: ** memdump.mem**
							Click Capture Memory
							
		5. Task Managerden taski sonlandirmaq ucun:
				Vm in ozunde "Help" in saginda ikinci icon clickle, Task Manageri sec, acilan windowda svchost.exe(32 bit) tap ve endtask et.
				Refresh Desktop
				
		### RegistryChangeView
			Open 
			compare registry
			Check HKEY_CURRENT_USER\Software or HKEY_LOCAL_MACHINE\Software (search for .....run)
				
		### Autopsy: disk image
					Create New Case:
						Case Name:
						Base Directory:
						Case Type: Single-user
						Case wil be stored in the following directory:

					New Case Information
						Case Number:
						Examiner:
						Finish

					Add Data Source:
						Select Data Source Type: Image or Vm File
						Browse for an image file: select (E01 file)
						Next
						Finish




		### Volatility: memory dump
		Copy memdump(Z:) and paste it in volatility folder
		
		# Help
				vol.py -h

		#u It list the processes of a system:

				vol.py -f ___.mem windows.pslist.PsList

		#viewing the process listing in tree form and using the same technique as pslist:

				vol.py -f ___.mem windows.pstree.PsTree
	
		WoW64 is a subsystem of the Windows operating system capable of running 32-bit applications on 64-bit Windows:
			Malicious process:
				vol.py -f ___.mem windows.pstree.PsTree | findstr True
		
		#memdump:

			vol.py -f ???/path/to/file??? -o ???/path/to/dir??? windows.memmap.Memmap ??????dump ??????pid <PID>

		#procdump:
			vol.py -f ???/path/to/file??? -o ???/path/to/dir??? windows.dumpfiles ??????pid <PID>
		
		
		
		### bstrings
			copy pid....dmp file to C:\4n6\Zimmerman\
			bstrings.exe -f pid....dmp
			
			# write to file:
				bstrings.exe -f pid....dmp -o .\res.txt
		
                        pslist

vol.py -f ???/path/to/file??? windows.pslist
vol.py -f ???/path/to/file??? windows.psscan
vol.py -f ???/path/to/file??? windows.pstree
procdump

vol.py -f ???/path/to/file??? -o ???/path/to/dir??? windows.dumpfiles ??????pid <PID>
Output differences:

Volatility 2: Just outputs specified PID (or all if not specified)
Volatility 3: Dumps exe and associated DLLs
memdump

vol.py -f ???/path/to/file??? -o ???/path/to/dir??? windows.memmap ??????dump ??????pid <PID>
dlls

vol.py -f ???/path/to/file??? windows.dlllist ??????pid <PID>
Output differences:

Volatility 2: PID, command line, base, size, loadcount, loadtime, path
Volatility 3: PID, process, base, size, name, path, loadtime, file output
cmdline

vol.py -f ???/path/to/file??? ??????profile <profile> cmdline
vol.py -f ???/path/to/file??? ??????profile <profile> cmdscan
vol.py -f ???/path/to/file??? ??????profile <profile> consoles
Output differences:

Volatility 2: process name, PID, commandline; cmdscan includes application, flags, process handle; consoles contains C:\ listing, original titles, screen position and command history information
Volatility 3: PID, process name, args
netscan

vol.py -f ???/path/to/file??? windows.netscan
vol.py -f ???/path/to/file??? windows.netstat
Note: The XP/2003 specific plugins are deprecated and therefore not available in Volatility 3

hivelist

vol.py -f ???/path/to/file??? windows.registry.hivescan
vol.py -f ???/path/to/file??? windows.registry.hivelist
hivedump

vol.py -f ???/path/to/file??? ??????profile <profile> printkey
malfind

vol.py -f ???/path/to/file??? windows.malfind
Output differences:

Volatility 2: PID, process name, address, VAD tags, hexdump, and shellcode
Volatility 3: PID, process name, process start, protection, commit charge, privatememory, file output, hexdump disassembly
yarascan

vol.py -f ???/path/to/file??? windows.vadyarascan ??????yara-rules <string>
vol.py -f ???/path/to/file??? windows.vadyarascan ??????yara-file ???/path/to/file.yar???
vol.py -f ???/path/to/file??? yarascan.yarascan ??????yara-file ???/path/to/file.yar???
