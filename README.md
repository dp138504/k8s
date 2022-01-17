# Kubernetes projects
This repo contains my personal Kubernetes projects hosted on my VMware Tanzu cluster.

## Completed
 - calibre-web: from [linuxserver/docker-calibre-web](https://github.com/linuxserver/docker-calibre-web)
   - calibre-web-books - Books library
   - calibre-web-comics - Comics library
 - home-assistant: from [linuxserver/docker-homeassistant](https://github.com/linuxserver/docker-homeassistant)
   > Note: Still need to migrate existing configuration over to k8s deployment.

## TODO
 
 - bitwarden

### Notes to self:
 - Use [this](https://rtyley.github.io/bfg-repo-cleaner/) to ensure secrets are cleaned up before pushing.
 - Use tig to improve traceability of file changes (`apt-get install tig` for install)