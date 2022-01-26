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
        

### Volatility: memory dump
