1. Take image of partition using FTK Imager:

			File > Create Disk Image:
						Select Source Window:
								Physical Drive
								Next
						Select Drive:
							"-----------" 
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
							Image Fragment Size: 0
							Finish
			Drive/Image Verify Results:
					Compare hashes

2. Run the malicious executable:

			Double-Click X:\malwex.exe
3. Restart VM
4. Capture the Memory using FTK Imager

			File > Capture Memory:
					Destination path: Z:\
					Destination filename: ** memdump.mem**
					Click Capture Memory

### Autopsy: disk image
			Create New Case:
				Case Name:
				Base Directory:
				Case Type: Single-user
				Case wil be stored in the following directory:
        

### Volatility: memory dump

# clarifing that which profile will be used.

`vol3.py -f ___.mem(path for memory dump) imageinfo`

#using this command you check all profiles which were found in "imageinfo" section. It list the processes of a system and you wil find correct profile.

vol3.py -f ___.mem --profile=Profile(exp. WinXPSP2x86) pslist 

#viewing the process listing in tree form and using the same technique as pslist
vol3.py -f ___.mem --profile=Profile pstree 

#searching  for commands that attackers entered through a console shell (cmd.exe)
vol3.py -f ___.mem --profile=Profile cmdscan 

#Similar to cmdscan. It not only prints the commands attackers typed, but it collects the entire screen buffer (input and output).
vol3.py -f ___.mem --profile=Profile consoles 

#viewing TCP connections that were active at the time of the memory acquisition
vol3.py -f ___.mem --profile=Profile connections 

#finding artifacts from previous connections that have since been terminated, in addition to the active ones
vol3.py -f ___.mem --profile=Profile connscan 

#detecting listening sockets for any protocol (TCP, UDP, RAW, etc)
vol3.py -f ___.mem --profile=Profile sockets 

#scanning for network artifacts
vol3.py -f ___.mem --profile=Profile netscan 

#dumping a process's executable
vol3.py -f ___.mem --profile=Profile procdump -D DIR(exp. /test_dump) --pid=PID(exp. 356) 


 *note1 ->  -D DIR (or --dump-dir=DIR) -> specifing an output directory 
 *note2 -> -p PID (or --pid=PID) ->displaying a a specific process instead of all processes

#showing you exactly which pages are memory resident
vol3.py -f ___.mem --profile=Profile memmap 

#extracting all memory resident pages in a process 
vol3.py -f ___.mem --profile=Profile memdump --pid=PID -D DIR

#showing process privileges
vol3.py -f ___.mem privs --profile=Profile 

#displaying a process's loaded DLL
vol3.py -f ___.mem --profile=Profile dlllist 

#extracting a DLL from a process's memory space and dump it to disk for analysis
vol3.py -f ___.mem --profile=Profile dlldump -D DIR 
