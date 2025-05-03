       ================================================================

       The Motorola - MaxTrac CONVENTIONAL - Radio Service Software
       (RSS) product, RVN-4019, has been updated as follows;

       Part #......................... RVN-4019-K
            includes 3.5" installation diskette
            RSS User's Manual #....... 68P8-0900Z03-J

       Software Version............... R07.02.00
       Software Date.................. 25-JUN-97

       ================================================================
       INSTALLATION:
       Motorola MaxTrac Conventional Mobile
       Radio Service Software (RSS):

       Insert the Installation Diskette into the A: -or- B: diskette
       drive, then Enter A: -or- B: at the DOS command prompt, to change
       to that drive as the "current working" drive.  Then Enter "INSTALL".
       Select the proper Disk Drive and SubDirectory for installation.

       !! CAUTION !!
       You cannot place the RSS SubDirectory in your DOS "PATH".  YOU MUST
       BE IN the RSS WORKING SubDirectory to properly execute the RSS (due
       to overlay loading).  The dummy batch file
               MAXTRAC.BAX
       is installed with the RSS during the RSS installation, and "points
       to" the TARGET Installation disk drive and directory.  This file is
       then copied to the root directory of your "C:" disk as file
               MAXTRAC.BAT

       IF YOU INSTALL THE RSS ON A NON-DEFAULT DRIVE and/or DIRECTORY,
       please EXAMINE this file for proper "path" drive/directory. 
       If you install to non-default disk, add "C:\" to the DOS "SET PATH="
       in your AUTOEXEC.BAT file, so the MAXTRAC.BAT file is found by DOS.
       ================================================================

  1. - !! CAUTION !! Attempting to use an un-formatted FLOPPY DISKETTE
       for archiving codeplugs will result in a fatal (RSS) DOS error #31. 
       See file DOS_INFO.DOC for using floppy diskettes for archiving, and
       for DOS error codes.

  2. - !! IMPORTANT !!  Please see file DOS_INFO.DOC for RSS/DOS/PC setup
       and trouble-shooting information.

  3. - !! IMPORTANT !!  The STACK size of this RSS has been increased,
       to enhance stability in a normal DOS environment (this does NOT affect
       execution memory requirements).

       If your environment includes elements which create abnormal
       quantities of hardware/software interrupts, then we STRONGLY
       recommend the following statement be inserted into your CONFIG.SYS
       file (DOS 3.2, 3.3, 4.x, 5.x, 6.x):

                          STACKS=9,512

       This tells DOS to furnish stack space to hardware interrupts which
       occur during RSS execution, thereby reducing the RSS stack loading, and
       avoiding errant DOS/application behaviours.  This statement MAY reduce
       the amount of conventional memory available by approximately 4 Kb. The
       number of stacks (9) can be increased to max. 64, if problems persist.

  4. - This RSS requires approximately 510 KB of free CONVENTIONAL
       memory for INITIAL execution.  However, more memory is dynamically
       allocated for functions such as codeplug and system-key reads (more
       files = more memory required), and if the RSS cannot allocate enough
       memory, an error message is given.  Make more memory available by
       using DOS "HIMEM.SYS" and "DOS=HIGH", and using DOS 5x/6x "MEM /C" to
       list memory allocations from CONFIG.SYS and AUTOEXEC.BAT, removing
       unnecessary items from those files.  This RSS does -NOT- require
       EXTENDED nor EXPANDED memory.

  5. - The "noems" argument to EMM386.EXE can prevent THIS RSS from executing
       properly on some PCs and versions of DOS.

       EMM386 can be used to free some CONVENTIONAL memory by allowing other
       drivers to be loaded into UPPER memory.  You can use the "ram" -or-
       "noems" switch to access UPPER memory.  Using the EMM386 "ram 64"
       switch to allocate the smallest-possible amount of EXPANDED memory
       (instead of using "noems") will allow THIS RSS to execute, when
       EMM386 is used only to load other drivers into UPPER memory.  Please
       consult DOS 'help emm386.exe' for information.

  6. - The PC-RIB-Radio Communications Timing has been changed, to
       enhance the Comm. Bus operation over a wider range of CPU speeds and
       Operating Systems (DOS, Windows).  This version contains 2 Timers
       which are independent of CPU speed, and which do not conflict
       directly with Windows' multi-tasking Timer when the RSS is used in
       Windows' FULL-SCREEN DOS MODE.

       If Reading or Writing the Radio's Codeplug causes a consistent
       failure on your PC, please see the WINDOWS item below, -and- the
       DOS_INFO.DOC file that was installed with this RSS, -BEFORE-
       contacting the Motorola Customer Resources RSS Support Team.

  7. - The RSS will now allow selection of Comm. Ports 1 - 4.  The
       Comm. Port selected must have a valid address in the PC BIOS Device
       Data Area (40:00 - 40:07), and the UART must be 8250/16450/16550
       compatible, or an error message "SELECTED PORT NOT VALID" is shown.
       If -no- valid port address is found in the BIOS area, the message
       "NO VALID PORT ADDRESS FOUND" is shown.

       If comm. ports are added to your PC, the proper Comm. Port I/O
       Addresses must be inserted into the PC BIOS Device Data Area, or the
       RSS will not recognize that Port as "valid". The I/O Address is a
       two-byte value (bytes are -reversed- in memory).  Most PC BIOS Start-Up
       routines will only scan and insert addresses for Comm. Ports 1 and 2.
       To add Comm. Ports 3 and 4, use the DOS "DEBUG" command, called in your
       AUTOEXEC.BAT file, and an ASCII text file of DEBUG commands in your
       C:\ directory (which you must create with a text-editor). This
       will allow DOS, Windows and the RSS to "see" the new Comm. Port(s).

       Use DOS command "MSD" to confirm adresses of existing Comm. Ports,
       prior to installing new Comm. Ports.


       -------------------------
       A)  C:\AUTOEXEC.BAT file;
       -------------------------

         rem *** call DEBUG w/Command File, set Comm. Port 3-4 Addresses
         debug  <c:\dbug_com.set


       -----------------------------------------------------------
       B)  C:\DBUG_COM.SET file (create this with text editor)

           // denotes comments, do -not- insert comments into file.
           The DEBUG command "?" will list command descriptions.
       -----------------------------------------------------------

         d 40:00 0F      // this dumps 1st 16 locations of BIOS Data Area
         e 40:04 E8 03   // set Comm Port -3- to Address 03E8 (bytes reversed)
         e 40:06 E8 02   // set Comm Port -4- to Address 02E8 (bytes reversed)
         d 40:00 0F      // this dumps 1st 16 locations of BIOS Data Area
         q               // this EXITS Debug, returns to DOS command prompt


       -----------------------------------------------------------
       The following are standard Comm. Port BIOS and I/O Addresses;
       
                   ROM BIOS DATA AREA  IBM PC/XT/AT    IBM PS/2 Series     

           COM1    40:00 - 40:01       03 F8 hex       03 F8 hex            
           COM2    40:02 - 40:03       02 F8 hex       02 F8 hex            
           COM3    40:04 - 40:05       03 E8 hex       32 20 hex            
           COM4    40:06 - 40:07       02 E8 hex       32 28 hex            

       Comm. ports should be installed at the appropriate addresses, and
       those addresses inserted into line(s) 3 (and 4) of C:\DBUG_COM.SET
       (above).  The RSS does not use UART interrupts, so the IRQ level on
       your Comm. Port card can be set to whatever does not conflict with
       your PC system's initial setup.  Some systems use IRQ4 for both COM1
       and COM3, and use IRQ3 for both COM2 and COM4 (on the premise that
       only 1 or 2 Comm. Ports are in use at one time).

       After the Comm. Port Addresses have been added to the BIOS DATA Area,
       the DOS "MODE" and "MSD" commands will also recognize the new ports.

  8. - The RSS will now initialize only the single Comm. Port that
       has been defaulted or selected.  Previously, the RSS would
       initialize both Comm. Ports 1 and 2 upon startup.  This change
       stops interference with a Comm. Port Mouse on an adjacent Comm. Port,
       and allows remote PC operations under third-party software.

  9. - WINDOWS - We cannot guaruntee successful operation of this RSS under
       Microsoft Windows ([*] = (tm) Microsoft Corp).  Windows will not
       allow programs direct access to the Comm. Port and Timer hardware;
       these functions are emulated by Windows, hence they are slower than
       under DOS, and this could interfere with critical communications
       timing.  Higher-speed CPUs/PCs (80486+ at 66 MHz and above) have the
       best chance of success.

       Any setup for RSS within Windows 3.1 [*] or Windows 95 [*] should be
       done in the DOS FULL-SCREEN Mode, as opposed to the DOS WINDOW Mode. 
       Communications programs (i.e. RSS Reading / Writing the Radio
       Codeplug) cannot be executed successfully in WINDOW "background" mode,
       and the WINDOW "foreground" mode may not sufficiently support the
       critical timing needed to consistently communicate with the
       RIB/Radio. FULL-SCREEN Mode gives higher priority (speed) to the RSS
       than the DOS WINDOW Mode.

       For Windows 3.1, use the PIF EDITOR to open the DOSPRMPT.PIF file.
       Set "Display Usage" to FULL SCREEN and "Execution" to EXCLUSIVE.
       Under "ADVANCED", set "Foreground Priority" to 10,000, and set the
       "Detect Idle Time" box OFF.  SAVE the file before using the
       "MS-DOS PROMPT" icon.

       For Windows 95, create an icon/shortcut.  Under PROPERTIES:
       Select PROGRAM Sheet;
           set "CLOSE ON EXIT" box TRUE.
           Under "ADVANCED";
               set "PREVENT PROGRAM FROM DETECTING WINDOWS" to TRUE.
               set "SUGGEST MS-DOS MODE" to FALSE.
               set "MS-DOS MODE" to FALSE.
       Select SCREEN Sheet;
           set "USAGE" to FULL SCREEN.
       Select MISC Sheet;
           set "ALLOW SCREENSAVER" to FALSE.
           set "IDLE SENSITIVITY" to LOW.

       If the above does not allow the RSS to function properly, then;
           a) EXIT Windows 3.1 and use normal DOS.
           b) Set Windows 95 PROGRAM/ADVANCED Sheet to "MS-DOS Mode".

 10. - Corrected CUSTOMER INFO Field during archive/backup of codeplug files;
       Now accepts upper/lower case, and the backup database file is
       properly updated.

 11. - ADDED Function "(F5/F8) PRINT Codeplug IMAGE Alignment Summary".
       Allows printing alignment data from RSS Codeplug IMAGE (memory) via
       the GET CODEPLUG FILE operations.  This allows printing of alignment
       data from a codeplug FILE (historical), in addition to (F5/F5)
       "ALIGNMENT SUMMARY from RADIO", which requires Radio attached to RIB
       and RSS during printing.

 12. - CodePlug READ Checksum Error 58 now expanded to Range 58-63.
       Give each Block unique checksum ID.

 13. - Corrected problem with I/O ACCESSORY CONNECTOR block in Codeplug;
       Now all unused pin entries are pre-zeroed.  This affects
       DESKTRAC RSS with DESKTRAC REPEATER Models.

 14. - Corrected LSTRING (2151) Error when entering (F4-F2) RADIO
       WIDE CONFIGURATION data screen, most often seen when using
       DOSSHELL to execute RSS.

 15. - Corrected Problem PLAsw15602, run-time error #2151, "LSTRING
       TOO LONG" when editing TX/RX Frequencies on Mode Screen.

 16. - Corrected Codeplug file UPDATES: now copies MODEL NUMBER field
       into MAXTRACM.DBF Database Catalog file, to support RE_ARCH.EXE.

 17. - Changed "Rx/Tx SQUELCH Code" fields on (F4/F5) "MODE CONFIGURATION"
       screen to accept -2- Non-Motorola DPL Codes, OCTAL 525 and 645,
       in addition to the standard Motorola DPL codes shown in RSS
       User's Guide.

       If DPL selected/entered is Non-Motorola code, a WARNING message
       is given that the code may not operate reliably.  Also, be
       careful of inverting non-standard DPL codes.

       !! WARNING !! Use of Non-Motorola DPL codes may result in erratic
       radio/system operation.  Motorola Inc. disclaims any and/or all
       liability for use of such non-standard codes.

 NOTE: This RSS is NO LONGER PACKAGED on 5.25" floppy diskettes.
       (C) Copyright MOTOROLA Inc. 1987, 1997.  All Rights Reserved.
