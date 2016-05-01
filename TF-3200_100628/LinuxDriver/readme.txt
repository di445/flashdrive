	      
	                   Linux Driver 

Contents:
-----------
1. File Description
2. Driver Installation for Linux
3. Driver Parameter
4. None EEPROM
5. EEPROM MP (OEM Only)

1. File Description
-------------------

Filename                Description
====================    =======================================================
sundance_main.c         Linux Driver Source Code.
                        This file is the main part of Linux Driver.

compat.h                Network interface message level settings.

crc32.h                 Crc function for early Linux 2.4.19pre kernel inclusion

ethtool.h:              Defines for Linux ethtool.

mii.h                   definitions for MII-compatible transceivers.

mii.c                   MII interface library.

makefile                Make File For IP100 Linux Driver.
                        Using "make all" for your kernel.

readme.txt              A summary of the contents for Linux Driver.
                        This file, which you are reading me now.



2. Driver Installation for Linux
-----------------------------------------
a. for kernel 2.4.x
   a1. Redhat 7.3 (linux kernel 2.4.18)
   a2. Mandrake 8.1 (kernel 2.4.8)
b. for kernel 2.6.x
c. automatically load and configure at next boot time

   a.for kernel 2.4.x
   -------------------
     a1. Redhat 7.3 (linux kernel 2.4.18)
     a1.1. install way 1:
         #make all =>generate sundance.o
         #cp sundance.o /lib/modules/2.4.18-3/kernel/drivers/net/
         #insmod ./sundance.o
         #ifconfig eth0 xxx.xxx.xxx.xxx netmask yyy.yyy.yyy.yyy
            eth0 is your network adapter,use "dmesg" to check it, ex: eth0, eth1...
            xxx  is your ip address, ex: 192.168.102.211
            yyy  is your netmask address, ex:255.255.255.0

     a1.2.  install way 2:
        #make all =>generate sundance.o
        #cp sundance.o /lib/modules/2.4.18-3/kernel/drivers/net/
        #insmod./sundance.o
        #setup
        [network configuration] =>to setup your ip address
        #ifup eth0
           eth0 is your network adapter, ex: eth0, eth1...	


     a2. Mandrake 8.1 (kernel 2.4.8)
       #make all  => generate sundance.o
       #cp sundance.o /lib/modules/2.4.8-26mdk/kernel/drivers/net
       #insmod ./sundance.o
       #ifconfig eth0 xxx.xxx.xxx.xxx netmask yyy.yyy.yyy.yyy
           eth0 is your network adapter,use "dmesg" to check it, ex: eth0, eth1...
           xxx  is your ip address, ex: 192.168.102.211
           yyy  is your netmask address, ex:255.255.255.0


   b. for kernel 2.6.x
   -------------------
      #make all  => generate sundance.ko
      #insmod ./sundance.ko (or sundance.o)
      #ifconfig eth0 xxx.xxx.xxx.xxx netmask yyy.yyy.yyy.yyy
            eth0 is your network adapter,use "dmesg" to check it, ex: eth0, eth1...
            xxx  is your ip address, ex: 192.168.102.211
            yyy  is your netmask address, ex:255.255.255.0      
   
   c. automatically load and configure at next boot time
   -----------------------------------------------------
     c1. cp sundance.o /lib/modules/`uname -r`/kernel/drivers/net
     *note: The `uname -r` is a command. Don't replace `uname -r` with
            2.4.18, 2.4.20smp, or some others. Must type `uname -r` directly.

     c2. Add the following lines at /etc/modules.conf:
	           
	      alias eth0 sundance
	      options sundance <optional parameters>
	           	           
     c3. Run "netconfig" or "netconf" to create configuration script 

              ifcfg-eth0 located at /etc/sysconfig/network-scripts or 
              create it manually.
              [see - Configuration Script Sample]

     c4. Driver will automatically load and configure at 
              next boot time.
              
     c5. Configuration Script Sample
     ===========================
         Here is a sample of a simple configuration script:

         DEVICE=eth0
         USERCTL=no
         ONBOOT=yes
         POOTPROTO=none
         BROADCAST=207.200.5.255
         NETWORK=207.200.5.0
         NETMASK=255.255.255.0
         IPADDR=207.200.5.2
              

3. Driver Parameter
-------------------
  If you want to change the link speed, you could use parameter after 
  insmod command.
  
  insmod sundance.o <optional parameter>    ; add parameter

  ========================================================================
   example: insmod sundance.o media=100mbps_hd
   or	    insmod sundance.o media=3
   or	    insmod sundance.o media=1,2,3,4	; for 4 cards or IP100
  ========================================================================              
  
  Parameter Description
  =====================
  You can install this driver without any addtional parameter. However, if 
  you are going to have extensive functions then it is necessary to set 
  extra parameter. Below is a list of the command line parameters supported 
  by the Linux device driver.

media=xxxxxxxxx			- Specifies the media type the NIC operates at.
				  autosense	Autosensing active media.
				  10mbps_hd	10Mbps half duplex.
				  10mbps_fd	10Mbps full duplex.
				  100mbps_hd	100Mbps half duplex.
				  100mbps_fd	100Mbps full duplex.
				  0		Autosensing active media.
				  1		10Mbps half duplex.
				  2		10Mbps full duplex.
				  3		100Mbps half duplex.
				  4		100Mbps full duplex.
				  By default, the copper devices operate at 
				  autosense, the fiber devices operate at
				  100Mbps full duplex.
				  Note that, the fiber adapter only support 
				  100Mbps half/full duplex types.	

  If wanting to change speed, this driver needed to be unloaded and reloaded with 
  new media parameter. Use rmmod to unload and insmod to reload driver.
  ========================================================================
   example: rmmod sundance.o 
   	    insmod sundance.o media=3
  ========================================================================    

flowctrl=[0|1]			- Specifies the flow control function.
				  0	Disable flow control.	
				  1	Enable flow control.	

4. None EEPROM
--------------
  If you want to use none eeprom solution. Please put EEPROM EEDO pin to GND.
  And, please add following -DNO_EEPROM define in Makefile, and re-compile again.

MAPPING_MODE= -DUSE_IO_OPS -DNO_EEPROM

5. EEPROM MP (OEM Only)
-----------------------
  This is a special tool for OEM embedded system to burn eeprom value with 
  MAC address. It is not for normal user. If you need this tool, please contact
  us directly. Thanks.
  
  5.1. unzip mp.zip and put 'mp directory' in the same directory with
  sundance_main.c

  5.2. Change Makefile:
  Form: "MAPPING_MODE= -DUSE_IO_OPS"
  To: "MAPPING_MODE= -DUSE_IO_OPS -DMP_EEPROM"

  Rebuild and load driver

  5.3. Read MAC address form EEPROM
  #cat /proc/ICPlus_eth0/IPF_EEPROM

  5.4. Write MAC address to EEPROM
  #echo "001122334455">/proc/ICPlus_eth0/IPF_EEPROM

  5.5. Convert EEPROM.TXT to eeprom_data.h
  run eep_cvrt.exe will convert EEPROM.txt to eeprom_data.h for linux driver
  use.