SGE
===

Sun Grid Engine Installtion

We have a binary of SGE which we use for installation rather than compiling it from source code, it is just to avoid dependency issue.

Binary Name: ge2011.11.tar.gz

Steps of installation :-

Master Node:
 adduser sge (SGE will not install if there is no user other than root)

 # iptables -F

 # chkconfig iptables –level 35 off

 make entry in /etc/hosts ( mention all hosts compute + master)

 # tar -xvfz ge2011.11.tar.gz

 # mv  ge2011.11 /opt/gridengine

 # cd /opt/gridengine

 # ./install_qmaster ( to configure master node )

 # cp /opt/gridengine/default/common/settings.sh /etc/profile.d/

 add PATH as /opt/gridengine/bin/linux-64/ in /etc/profile

 # source /etc/profile

 # qconf -ah compute-node2 ( add compute nodes )

 # qconf -ah compute-node3

 # qstat -f ( it will show all the added compute nodes )

        queuename                      qtype resv/used/tot. load_avg arch          states
        ---------------------------------------------------------------------------------
        all.q@compute-node2               BIP   0/0/2          0.00     linux-x64     
        ---------------------------------------------------------------------------------
        all.q@compute-node3              BIP   0/0/1          0.00     linux-x64     


 # scp -r /opt/gridengine compute-node2:/opt

 # scp -r /opt/gridengine compute-node3:/opt

Compute Node:
 # iptables -F

 # chkconfig iptables –level 35 off

 make entry in /etc/hosts ( mention all hosts compute + master)

 # cd /opt/gridengine

 # ./install_execd ( to configure compute node and tell it its master node)

 # cp /opt/gridengine/default/common/settings.sh /etc/profile.d/

 add PATH as /opt/gridengine/bin/linux-64/ in /etc/profile/

 # source /etc/profile

 # qstat -f ( it will show all the added compute nodes )

      queuename                      qtype resv/used/tot. load_avg arch          states
      ---------------------------------------------------------------------------------
      all.q@compute-node2               BIP   0/0/2          0.00     linux-x64     
      ---------------------------------------------------------------------------------
      all.q@compute-node3              BIP   0/0/1          0.00     linux-x64     
