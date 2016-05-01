

           TP-LINK TF-3200 10/100 Fast Ethernet Adapter
                    Novell ODI Server Driver


Contents:
---------

1. File Description
2. Driver Installation for NetWare Server
3. Parameters Description


1. File Description
-------------------

Filename              Description
=================     =====================================================
README.TXT            Presents a summary of the contents for NetWare Server
                      driver installation.

IPFSRV.LAN            Server ODI Driver
                      This driver complies with NetWare ODI Server driver
                      SPEC 3.31.

IPFSRV.LDI            The driver installation file for Netware 6.x/
                      Netware 5.x/Netware 4.x.

4.X\NBI.NLM           NetWare Server 4.X Bus Interface module.

4.X\MSM.NLM           NetWare Server 4.X LAN driver Media Support
                      Module (MSM).

4.X\ETHERTSM.NLM      NetWare Server 4.X LAN driver Topology Specific Module
                      (TSM) for Ethernet.


2. Driver Installation for NetWare Server
-----------------------------------------

    ** Driver Installation for NetWare Server 4.X **

         a. Update Netware Server to 4.2 .
            (If dont update to 4.2, use diskette update file "MSM.NLM,
             ETHERTSM.NLM")
         b. Run NetWare Server System .
         c. When the Server prompt appears, load the NetWare Server
            Installation Utility ==> "LOAD INSTALL"
         d. Select "Driver options" from the "Installtion Options" menu.
         e. Select "Configure network drivers" from the "Driver Options" menu.
         f. Select "Select a driver" from the "Additional Driver Actions" menu
         g. Press <Ins> to install a unlisted driver, then press <F3> to
            specify a different path.
         h. Insert Driver Diskette in your PC's floppy drive and specify
            the path A:\NOVELL\SERVER.
         i. Select "TP-LINK TF-3200 10/100 Fast Ethernet Adapter" from
            the "Select a driver to install:" menu.
         j. If necessary, select "Select/Modify driver parameters and
            protocols" from the "Board IPFSRV_1 (Driver IPFSRV) Actions" memu.
         k. Follow instructions to complete driver installation.

       ***ps: If the system already have one or more Network cards installed, the 
              installation may not be completed for the resource allocation
              problem. To solve this problem, please add the following 3 lines into 
              STARTUP.NCF file :
              # set maximum packet receive buffers = 2000
              # set minimum packet receive buffers = 256
              # set maximum physical  receive packet buffers = 2048
 

    ** Driver Installation for NetWare Server 5.X/6.X **

         a. Run NetWare Server System .
         b. When the Server prompt appears, load the NetWare Server
            Installation Utility ==> "LOAD NWCONFIG"
         c. Select "Driver options" from the "Installtion Options" menu.
         d. Select "Configure network drivers" from the "Driver Options" menu.
         e. Select "Select a driver" from the "Additional Driver Actions" menu
         f. Press <Ins> to install a unlisted driver, then press <F3> to
            specify a different path.
         g. Insert Driver Diskette in your PC's floppy drive and specify
            the path A:\NOVELL\SERVER.
         h. Select "TP-LINK TF-3200 10/100 Fast Ethernet Adapter" from the
            "Select a driver to install:" menu.
         i. If necessary, select "Select/Modify driver parameters and
            protocols" from the "Board IPFSRV_1 (Driver IPFSRV) Actions" memu.
         j. Follow instructions to complete driver installation.

            Sample AUTOEXEC.NCF for NetWare Server

             AUTOEXEC.NCF (one board)
             ========================
              LOAD IPFSRV SLOT=2 FRAME=ETHERNET_802.2 NAME=TMI_8022
              LOAD IPFSRV SLOT=2 FRAME=ETHERNET_802.3 NAME=TMI_8023
              LOAD IPFSRV SLOT=2 FRAME=ETHERNET_II NAME=TMI_II
              LOAD IPFSRV SLOT=2 FRAME=ETHERNET_SNAP NAME=TMI_SNAP
              BIND IPX TMI_8022 NET=10
              BIND IPX TMI_8023 NET=20
              BIND IPX TMI_II   NET=30
              BIND IPX TMI_SNAP NET=40


3. Parameter Description
------------------------

    The following parameters are used in IPFSRV.LAN.

    a. SLOT  : Specifies which adapter is enabled when multiple adapters
               are found in your computer.

                Ex: LOAD IPFSRV SLOT=3 FRAME=ETHERNET_802.2
                    LOAD IPFSRV SLOT=4 FRAME=ETHERNET_II

    b. FRAME : Specifies which frame type is used by the driver.  Accepted
               values are Ethernet_802.2, Ethernet_802.3, Ethernet_II and
               Ethernet_SNAP.

                Ex: LOAD IPFSRV FRAME=ETHERNET_802.2
                    LOAD IPFSRV FRAME=ETHERNET_802.3
                    LOAD IPFSRV FRAME=ETHERNET_II
                    LOAD IPFSRV FRAME=ETHERNET_SNAP

    c. NODE  : Use a different address to replace the node address burned
               in EEPROM.

               Ex: LOAD IPFSRV NODE=004095888888

    4. SPEED : Specifies which medium type is used by the driver.
               Accepted vaules are AUTOSENSE, 10BASET, 10BASETFD,
               100BASETX, 100BASETXFD.

               Ex: LOAD IPFSRV AUTOSENSE

    5. VLAN  : Select VLAN ID. (Decimal Value)
               The valid range is 1 to 4095h.

               Ex: LOAD IPFSRV VLANId=1

