# coredns

Set your local IP:
```bash
LOCAL_IP=$(ip a s $(ip r | head -n 1 | awk '{print $5}') | awk '/inet/ {print $2}' | cut -d / -f 1 | head -n 1)
```

Update your local IP:
```bash
sed "s/8.8.8.8/${LOCAL_IP}/g" -i docker-compose.yml
```

Start the CoreDNS server:
```bash
docker-compose up -d
```

Test the CoreDNS server:
```bash
host nginx.shubham.local ${LOCAL_IP}
```

---

Revert changes:
```bash
sed "s/${LOCAL_IP}/8.8.8.8/g" -i docker-compose.yml
```

Test your DNS resolution:
```bash
host nginx.shubham.local 192.168.1.16
```
> `192.168.1.16` is the DNS server IP.

