# Bash Scripts Collection 🔨

Practical bash scripts for system administration tasks.

## Scripts

### system-info.sh
Displays system information at a glance.
```bash
#!/bin/bash
echo "=============================="
echo "   SYSTEM INFORMATION"
echo "=============================="
echo "Hostname  : $(hostname)"
echo "OS        : $(cat /etc/os-release | grep PRETTY_NAME | cut -d= -f2)"
echo "Kernel    : $(uname -r)"
echo "Uptime    : $(uptime -p)"
echo "IP Address: $(hostname -I | awk '{print $1}')"
echo "RAM       : $(free -h | awk '/Mem:/ {print $3 "/" $2}')"
echo "Disk      : $(df -h / | awk 'NR==2 {print $3 "/" $2}')"
echo "=============================="
```

### backup.sh
Simple directory backup with timestamp.
```bash
#!/bin/bash
SOURCE=$1
DEST="/home/$(whoami)/backups"
DATE=$(date +%Y%m%d_%H%M%S)

mkdir -p $DEST
tar -czf "$DEST/backup_$DATE.tar.gz" "$SOURCE"
echo "Backup created: backup_$DATE.tar.gz"
```

### port-checker.sh
Check if common ports are open on a target.
```bash
#!/bin/bash
TARGET=$1
PORTS=(22 80 443 8080 3306)

echo "Scanning $TARGET..."
for PORT in "${PORTS[@]}"; do
    (echo >/dev/tcp/$TARGET/$PORT) 2>/dev/null \
      && echo "Port $PORT: OPEN" \
      || echo "Port $PORT: CLOSED"
done
```

## How to Use
```bash
chmod +x script-name.sh    # Make executable
./system-info.sh            # Run it
./backup.sh /path/to/dir   # Backup a directory
./port-checker.sh 10.0.0.1 # Scan ports
```

*More scripts coming soon!*
