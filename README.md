SGE
===

Sun Grid Engine Installtion

We have a binary of SGE which we use for installation rather than compiling it from source code, it is just to avoid dependency issue.

Binary Name: ge2011.11.tar.gz


Steps of installation :-

Master Node:
1. adduser sge (SGE will not install if there is no user other than root)
2. # iptables -F
3. # chkconfig iptables –level 35 off
4. make entry in /etc/hosts ( mention all hosts compute + master)
5. # tar -xvfz ge2011.11.tar.gz
6. # mv  ge2011.11 /opt/gridengine
7. # cd /opt/gridengine
8. # ./install_qmaster ( to configure master node )
9. # cp /opt/gridengine/default/common/settings.sh /etc/profile.d/
10. add PATH as /opt/gridengine/bin/linux-64/ in /etc/profile
11. # source /etc/profile
12. # qconf -ah compute-node2 ( add compute nodes )
13. # qconf -ah compute-node3
14. # qstat -f ( it will show all the added compute nodes )

        queuename                      qtype resv/used/tot. load_avg arch          states
        ---------------------------------------------------------------------------------
        all.q@compute-node2               BIP   0/0/2          0.00     linux-x64     
        ---------------------------------------------------------------------------------
        all.q@compute-node3              BIP   0/0/1          0.00     linux-x64     


15.  # scp -r /opt/gridengine compute-node2:/opt
16.  # scp -r /opt/gridengine compute-node3:/opt

Compute Node:
1. # iptables -F
2. # chkconfig iptables –level 35 off
3. make entry in /etc/hosts ( mention all hosts compute + master)
4. # cd /opt/gridengine
5. # ./install_execd ( to configure compute node and tell it its master node)
6. # cp /opt/gridengine/default/common/settings.sh /etc/profile.d/
7. add PATH as /opt/gridengine/bin/linux-64/ in /etc/profile/
8. # source /etc/profile
9. # qstat -f ( it will show all the added compute nodes )
      
      
      queuename                      qtype resv/used/tot. load_avg arch          states
      ---------------------------------------------------------------------------------
      all.q@compute-node2               BIP   0/0/2          0.00     linux-x64     
      ---------------------------------------------------------------------------------
      all.q@compute-node3              BIP   0/0/1          0.00     linux-x64     
