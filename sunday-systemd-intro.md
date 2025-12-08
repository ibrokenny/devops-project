# Date: [Sunday]
Time: 9:00pm - 9:45pm

## Commands Learned 

#Status Checks
--systemctl status [service e.g sshd/firewalld]
--systemctl list-units --type=service
--systemctl -s-enabled [service]

##Control Services 
--systemctl start [service]
--systemctl stop [service]
--systemctl restart [service]
--systemctl reload [service]


## Boot Persistence
--systemctl enable [service]
--systemctl disable [service]
systemctl enable --now [service] (enable + start)
--systemctl disable --now [service] (disable + stop)

## practice Service 
I used firewalld for practice( safe, non-critical)

## Understanding 
--systemd manages services in Linux
--Services can run (active) or be stopped (inactive)
--Services can be enabled (start at boot) or disabled 
--status show current state + recent logs

## Next Practice 
--View logs with journalctl 
--Create custom service
-- Troubleshoot failed services 

# I transfered this file from my system using the netcat commnad 

netcat -l 1234 > sunday-systemd-intro.md, this on the system where the file exist.then
cat sunday-systemd-intro.md | netcat ipaddress port number(1234) -q 0

