# SSH tunnel
```bash
# Attacker:
ssh -L LOCAL_PORT:SERVICE_IP:SERVICE_PORT USER@TARGET_IP
```

# Socat
```bash
# Target
socat tcp-listen:LOCAL_PORT,reuseaddr,fork tcp:SERVICE_IP:SERVICE_PORT
```