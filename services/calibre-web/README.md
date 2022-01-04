# calibre-web

To install:
1) `kubectl create ns calibre-web`
2) `kubectl apply -f calibre-web-books-pv.yml`
3) `kubectl apply -f calbire-web-books-pvc.yml -n calibre-web`
> Note: Ensure `kubectl get pv,pvc -n calibre-web` shows `Bound` for both the `calibre-web-books-config-pv` and `calibre-web-books-config-pvc`
4) `kubectl apply -f . -n calibre-web`
