              TP-LINK TF-3200 10/100 Fast Ethernet Adapter
                      Novell DOS ODI Driver

Contents:
---------

1. File Description
2. Driver Installation for Novell DOS client
3. Parameters Description


1. File Description
-------------------

Filename      Description
==========    ================================================================
IPFODI.COM    Novell DOS ODI driver.
              This driver is designed for DOS ODI driver. Using this driver, 
              you can login into Novell Netware server and access server's
              files in DOS environment.

NET.CFG       Novell DOS client Configuration File.
              You can change client's speed and binding protocol by this file.

README.TXT    A summary of the contents for Novell DOS ODI driver.
              This file, which you are reading now.


2. Driver Installation for Novell DOS client
--------------------------------------------

    ** Driver Installation for Dos **
         a. Boot up Novell Server.
            First at all, you need to boot up Novell Server. 

         b. Need file for Novell DOS client.
            LSL.COM, IPXODI.COM, VLM.COM, and VLM.COM necessary file.

         c. Login into Novell Server.
            Boot client computer into DOS mode. Typing following command, you 
            would  touch novell server.
            
            LSL.COM
            IPFODI.COM
            IPXODI.COM
            VLM.COM
            login admin

            The LSL.COM is Link Support Layer. 
            The IPFODI.COM is my adapter driver. 
            The IPXODI.COM is IPX protocol layer binding on IPFODI driver. 
            The VLM.COM is NetWare virtual loadable module manager.
    
         d. Unload Novell Dos Client. 
            After finish your job, you can unload you Novell dos client, using
            following command:

            logout
            VLM u
            IPXODI u
            IPFODI u
            LSL u
           
3. Parameters Description
-------------------------
    
    ** Change Link Speed **
     a. Using NET.CFG you change link speed and half/full duplex mode.  You can 
        not open two speed at the same time. Using ';' to mark the speed modes 
        which you don't need. For example, if you wanted to using 10Mb Half mode:

        ;AUTOSENSE         
        10BaseT        
        ;10BaseTFD        
        ;...


	 b. There are available speed mode.
         Speed Mode           Descrtion
         ================     ================================================
         AUTOSENSE            ;Performs Power-Up Autosense on all types of boards
                              ;in order to connect to the active line, and dynamic 
                              ;10/100 autosensing (at run-time) on boards 
                              ;Supporting it.

         10BaseT              ;Select 10Mbps half duplex Force mode.

         10BaseTFD            ;Select 10Mbps full duplex Force mode.

         100BaseTX            ;Select 100Mbps half duplex Force mode.

         100BaseTXFD          ;Select 100Mbps full duplex Force mode.


    ** Change Link Protocol **

          There four frame type that you can bind to IPFODI driver. These four frame
          type can be binded to IPFODI driver at the same time, but you need to bind
          at least one protocol which your Novell Server provide now. Also using ';'
          to mark the protocol you don't need.

          Frame        Ethernet_802.2  
          Frame        Ethernet_802.3  
          Frame        Ethernet_II     
          Frame        Ethernet_snap   

    ** Flow Control **
          
          The default value of Flow Control is "Enabled". User can use 
          "DISABLE_FLOWCONTROL" to disable Flow Control.
          
          DISABLE_FLOWCONTROL   ; disable flow control