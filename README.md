# stream-relay

## Prep

    apt-get update
    apt-get dist-upgrade
    apt-get install nano build-essential git tcl libssl1.0-dev nodejs npm usb-modeswitch libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev cmake joe screen

## Firewall clear-out

    #!/bin/bash
    
    iptables-save > iptables.backup
    iptables -P INPUT ACCEPT
    iptables -P OUTPUT ACCEPT
    iptables -P FORWARD ACCEPT
    iptables -F
    iptables --flush

## srt-relay.sh

    #!/bin/bash
    
    /home/ubuntu/srt/srt-live-transmit -st:yes "srt://0.0.0.0:5005?mode=listener&lossmaxttl=40&latency=2000" "srt://0.0.0.0:5006?mode=listener" 1> /home/ubuntu/srt-output1.log 2> /home/ubuntu/srt-error1.log &

## srtla-relay.sh

    #!/bin/bash
    
    /home/ubuntu/srtla/srtla_rec 5000 127.0.0.1 5002 &
    /home/ubuntu/srt/srt-live-transmit -st:yes "srt://127.0.0.1:5002?mode=listener&lossmaxttl=40&latency=2000" "srt://0.0.0.0:5001?mode=listener"
