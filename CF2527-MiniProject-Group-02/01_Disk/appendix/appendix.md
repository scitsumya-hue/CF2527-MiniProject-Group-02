# APPENDIX — COMPUTER FORENSICS DRIVE IMAGE INVESTIGATION

## Supporting Screenshots and Evidence

This appendix contains the Autopsy 4.23.1 evidence-analysis screenshots captured during the forensic examination of the acquired hard drive image.

### Appendix A — Evidence Source

This section documents the acquired data source and its core image properties as recorded by Autopsy.

![Figure A1 - Autopsy listing of the data source](images/Drive_Figure_A1.png)

**Figure A1.** Autopsy “Listing” view of data source jo-2009-11-20-oldComputer.E01, showing image type “Image”, size 13,020,069,888 bytes, sector size 512 bytes, timezone Asia/Calcutta, and Device ID 2802913c-930a-4e2d-9aaf-b8b11afda896.

### Appendix B — Operating System / Computer Identification

The Operating System Information artifact identifies the host computer name, installed operating system, and registered owner details recovered from the system registry.

![Figure B1 - Operating System Information artifact](images/Drive_Figure_B1.png)

**Figure B1.** Operating System Information artifact showing Name “M57-JO”, Program Name “Microsoft Windows XP Service Pack 3”, Processor Architecture “x86”, Product ID “76487-027-5250835-22087”, Owner “Jo”, and Organization “M57.biz”, recovered from the Windows registry (source: Recent Activity).

### Appendix C — Browser / Web Activity

Autopsy's Web History module recovered 3,733 browsing records from the Firefox places.sqlite database, documenting user internet activity on the system.

![Figure C1 - Web History results](images/Drive_Figure_C1.png)

**Figure C1.** Web History results (3,733 records) with entry http://www.mozilla.com/firefox selected, showing Date Accessed 2009-11-13 07:19:28 IST, Domain mozilla.com, and Program Name “FireFox Analyzer”, recovered from /vol_vol2/Documents and Settings/Jo/Application Data/Mozilla/Firefox/Profiles/4pglibt6.default/places.sqlite.

### Appendix D — USB Devices / Removable Media

The USB Device Attached artifact identified 11 distinct USB connection events recovered from the SYSTEM registry hive, documenting removable media and peripherals connected to the host.

![Figure D1 - USB Device Attached results](images/Drive_Figure_D1.png)

**Figure D1.** USB Device Attached results (11 results) with entry selected showing Date/Time 2009-11-20 06:37:33 IST, Device Make “Logitech, Inc.”, Device Model “Optical Wheel Mouse”, and Device ID 5&2f6f8af0&0&2, recovered from /vol_vol2/WINDOWS/system32/config/system. Other entries include an Alcor Micro Corp. flash drive, a LaCie rugged mobile hard drive, an Imation Corp. flash drive, and a Dell keyboard and mouse.

### Appendix E — Evidence Reference

| Item | Reference |
|---|---|
| Case name | `CF_DriveImage_Investigation` |
| Evidence file | `jo-2009-11-20-oldComputer.E01` |
| Device ID | `2802913c-930a-4e2d-9aaf-b8b11afda896` |
| Forensic tool | Autopsy 4.23.1 |
