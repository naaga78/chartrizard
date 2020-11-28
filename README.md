# chartrizard
Helm repo

This repository contains Helm charts for various projects

* [Application 1](charts/app1/)
* [Sonarr](charts/sonarr/)
* [Radarr](charts/radarr/)
* [Jackett](charts/jackett/)
* [Transmission](charts/transmission-openvpn/)

## Installing Charts from this Repository

Add the Repository to Helm:

    helm repo add chartrizard https://naaga78.github.io/chartrizard/
    helm repo update

Install Application 1:

    helm install 'name' chartrizard/app1 

Install Sonarr:

    helm install 'name' chartrizard/sonarr --values media.sonarr.values.yml --namespace media

Install Radarr:

    helm install 'name' chartrizard/radarr --values media.radarr.values.yml --namespace media

Install Jackett:

    helm install 'name' chartrizard/jackett --values media.jackett.values.yml --namespace media

Install Transmission:

    helm install 'name' chartrizard/transmission-openvpn --values media.transmission-openvpn.values.yml --namespace media