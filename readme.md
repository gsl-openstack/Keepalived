#Installing keepalived
root@Controller01:~#apt-get install keepalived 
root@Controller01:~#vim etc/keepalived/keepalive.conf
global_defs {<br/>
router_id xit<br/>
}<br/>
vrrp_script haproxy {<br/>

script "killall -0 haproxy"<br/>
  interval 2<br/>
  weight 2<br/>
}<br/>
vrrp_instance 40{<br/>
  virtual_router_id 40<br/>
  advert int 1<br/>
  priority 101<br/>
  state MASTER<br/>
  interface ens18<br/>
  virtual_ipaddress {<br/>
    10.74.75.124 dev ens18<br/>
  }<br/>
  track_script {<br/>
    haproxy<br/>
  }<br/>
}<br/>
 track_script {<br/>
    haproxy<br/>
  }<br/>

 -add above configuration on all the controller node<br/>.
 root@Controller01:~#systemctl keepalived restart 