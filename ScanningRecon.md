    https://net.cybbh.io/-/public/-/jobs/878264/artifacts/modules/networking/slides-v4/07_discovery.html
_________________________________________________________________________________________________________________
    https://net.cybbh.io/public/networking/latest/07_discovery/fg.html
_________________________________________________________________________________________________________________
- ping sweep
  
        for i in {1..254}; do (ping -c 1 X.X.X.$i | grep "bytes from" &) ; done

- nmap -sV -Pn -T4 [IP]

        nmap -Pn [IP/CIDR] -T5 -p[21-23,80] --open

- sudo traceroute [IP] -p [port]

        tbd

- nc [Options] [Target IP] [Target Port(s)]

        nc -zvnw1 [IP] [port]
_________________________________________________________________________________________________________________
- Netcat TCP scan script

        #!/bin/bash
        echo "Enter network address (e.g. 192.168.0): "
        read net
        echo "Enter starting host range (e.g. 1): "
        read start
        echo "Enter ending host range (e.g. 254): "
        read end
        echo "Enter ports space-delimited (e.g. 21-23 80): "
        read ports
        for ((i=$start; $i<=$end; i++))
        do
            nc -nvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
        done

- Netcat UDP scan script
 
        #!/bin/bash
        echo "Enter network address (e.g. 192.168.0): "
        read net
        echo "Enter starting host range (e.g. 1): "
        read start
        echo "Enter ending host range (e.g. 254): "
        read end
        echo "Enter ports space-delimited (e.g. 21-23 80): "
        read ports
        for ((i=$start; $i<=$end; i++))
        do
            nc -nuvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
        done
_________________________________________________________________________________________________________________
- curl

        curl [IP:port]

- wget

        wget -r [IP:port]
_________________________________________________________________________________________________________________
- DEV TCP Banner grab

        exec 3<>/dev/tcp/[IP]/[port]; echo -e "" >&3; cat <&3

- DEV TCP Scanning

        for p in {1..1023}; do(echo >/dev/tcp/[IP]/$p) >/dev/null 2>&1 && echo "$p open"; done
_________________________________________________________________________________________________________________
