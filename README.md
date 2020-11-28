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

    helm install chartrizard/app1

Install Sonarr:

    helm install chartrizard/sonarr

Install Radarr:

    helm install chartrizard/radarr

Install Jackett:

    helm install chartrizard/jackett

Install Transmission:

    helm install chartrizard/transmission-openvpn