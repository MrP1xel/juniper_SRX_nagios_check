import subprocess
import sys
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("-cpu", help="CPU average")
parser.add_argument("-host", help="host IP")
parser.add_argument("-community", help="SNMP community of the device")
parser.add_argument("-warning", help="warning level")
parser.add_argument("-critical", help="critical level")
args = parser.parse_args()

hostIp = ""
community = ""

if args.warning :
        WARNING_LEVEL = args.warning

if args.critical:
        CRITICAL_LEVEL = args.critical

if args.community:
        community = args.community
if args.host:
        hostIp = args.host

def get_cpu_average():
        resultat = []
        cmd = "snmpwalk -c " + community +" " + " -v 2c 172.17.43.12 1.3.6.1.4.1.2636.3.1.13.1.20.9.1.0 " + hostIp
        output1m = subprocess.check_output(cmd,shell=True)
        value1m = output1m.split("=")[1].split(":")[1]
        resultat.append(value1m)
        cmd = "snmpwalk -c " + community +" " + " -v 2c 172.17.43.12 1.3.6.1.4.1.2636.3.1.13.1.21.9.1.0 " + hostIp
        output5m = subprocess.check_output(cmd,shell=True)
        value5m = output5m.split("=")[1].split(":")[1]
        resultat.append(value5m)
        cmd = "snmpwalk -c " + community +" " + " -v 2c 172.17.43.12 1.3.6.1.4.1.2636.3.1.13.1.22.9.1.0 " + hostIp
        output15m = subprocess.check_output(cmd,shell=True)
        value15m = output15m.split("=")[1].split(":")[1]
        resultat.append(value15m)
        return resultat

if args.cpu :
        values = get_cpu_average()
        cpu1m =values[0]
        cpu5m =values[1]
        cpu15m = values[2]
        if int(max(values).strip()) >= int(CRITICAL_LEVEL) :

                print "CRITICAL- 1m:%s%% 5m:%s%% 15m:%s%%|cpu_average_1m=%s cpu_average_5m=%s cpu_average_15m=%s" % (cpu1m.strip(),cpu5m.strip(),cpu15m.strip(),cpu1m.strip() ,cpu5m.strip() ,cpu15m.strip())
                sys.exit(2)
        else :
                if int(max(values).strip()) >= int(WARNING_LEVEL) :
                        print "WARNING - 1m:%s%% 5m:%s%% 15m:%s%%|cpu_average_1m=%s cpu_average_5m=%s cpu_average_15m=%s" % (cpu1m.strip(),cpu5m.strip(),cpu15m.strip(),cpu1m.strip() ,cpu5m.strip() ,cpu15m.strip())
                        sys.exit(1)
                else:
                        print "OK - 1m:%s%% 5m:%s%% 15m:%s%%|cpu_average_1m=%s cpu_average_5m=%s cpu_average_15m=%s" % (cpu1m.strip(),cpu5m.strip(),cpu15m.strip(),cpu1m.strip() ,cpu5m.strip() ,cpu15m.strip())
                        sys.exit(0)
