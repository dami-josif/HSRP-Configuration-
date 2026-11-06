# HSRP-Configuration-
Hot Standby Router Protocol HSRP
Part 2: Configure HSRP Active and Standby Routers
Step 1: Configure HSRP on R1.
a. Configure HSRP on the G0/1 LAN interface of R1.
Open configuration window
R1(config)# interface g0/1
b. Specify the HSRP protocol version number. The most recent version is version 2.
Note: Standby version 1 only supports IPv4 addressing.
R1(config-if)# standby version 2
c. Configure the IP address of the virtual default gateway. This address must be configured on any hosts
that require the services of the default gateway. It replaces the physical interface address of the router
that has been previously configured on the hosts.
Multiple instances of HSRP can be configured on a router. You must specify the HSRP group number to
identify the virtual interface between routers in a HSRP group. This number must be consistent between
the routers in the group. The group number for this configuration is 1.
R1(config-if)# standby 1 ip 192.168.1.254
d. Designate the active router for the HSRP group. It is the router that will be used as the gateway device
unless it fails or the path to it becomes inactive or unusable. Specify the priority for the router interface.
The default value is 100. A higher value will determine which router is the active router. If the priorities of
the routers in the HSRP group are the same, then the router with the highest configured IP address will
become the active router.
R1(config-if)# standby 1 priority 150
R1 will operate as the active router and traffic from the two LANs will use it as the default gateway.
e. If it is desirable that the active router resume that role when it becomes available again, configure it to
preempt the service of the standby router. The active router will take over the gateway role when it
becomes operable again.
R1(config-if)# standby 1 preempt
Question:
What will the HSRP priority of R3 be when it is added to HSRP group 1?

Step 2: Configure HSRP on R3.
Configure R3 as the standby router.
a. Configure the R3 interface that is connected to LAN 2.
b. Repeat only steps 1b and 1c above.
Step 3: Verify HSRP Configuration
a. Verify HSRP by issuing the show standby command on R1 and R3. Verify the values for HSRP role,
group, virtual IP address of the gateway, preemption, and priority. Note that HSRP also identifies the
active and standby router IP addresses for the group.
R1# show standby

Part 3: Observe HSRP Operation
Step 1: Make the active router become unavailable.
Open a command prompt on PC-B and enter the command tracert 209.165.200.226.
Question:
Does the path differ from the path used before HSRP was configured?
Type your answers here.
Step 2: Break the link to R1.
a. Select the delete tool from the Packet Tracer toolbar and delete the cable that connect s R1 to S1.
b. Immediately return to PC-B and execute the tracert 209.165.200.226 command again. Observe the
output of the command until the command completes execution. You may need to repeat the trace to see
the full path.
Question:
How was this trace different from the previous trace?
HSRP undergoes a process to determine which router should take over when the active router becomes
unavailable. This process takes time. Once the process is complete, the R3 standby router becomes
active and is used as the default gateway for hosts on LAN 1 and LAN 2.
Step 3: Restore the link to R1.
a. Re-connect R1 to S1 with a copper straight-through cable.
b. Execute a trace from PC-B to the Web Server. You may need to repeat the trace to see the full path.
Questions:
What path is used to reach the Web Server?
If the preempt command was not configured for the HSRP group on R1, would the results have been thesame?
