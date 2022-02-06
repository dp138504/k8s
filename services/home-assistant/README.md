# home-assistant

To install:
1) Edit `homeassistant-cfgmap.yml` to include correct Pod and Node CIDR ranges.
1) `kubectl create ns home-assistant`
2) `kubectl apply -f . -n home-assistant`
3) Ensure web frontend is reachable via HTTPProxy ingress.

