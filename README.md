# chartrizard
Helm repo

This repository contains Helm charts for various projects

* [Sonarr](charts/sonarr/)
* [Radarr](charts/radarr/)
* [Lidarr](charts/lidarr/)
* [Jackett](charts/jackett/)
* [Transmission](charts/transmission-openvpn/)
* [Ubooquity](charts/ubooquity/)
* [Ombi](charts/ombi/)


## Installing Charts from this Repository

Add the Repository to Helm:

    helm repo add chartrizard https://naaga78.github.io/chartrizard/
    helm repo update


Install Sonarr:

    helm install sonarr chartrizard/sonarr --values media.sonarr.values.yml --namespace media

Install Radarr:

    helm install radarr chartrizard/radarr --values media.radarr.values.yml --namespace media

Install Lidarr:

    helm install lidarr chartrizard/lidarr --values media.lidarr.values.yml --namespace media

Install Jackett:

    helm install jackett chartrizard/jackett --values media.jackett.values.yml --namespace media

Install Transmission:

    helm install transmission chartrizard/transmission-openvpn --values media.transmission-openvpn.values.yml --namespace media

Install Ubooquity:

    helm install ubooquity chartrizard/ubooquity --values media.ubooquity.values.yml --namespace media

Install Ombi:

    helm install ombi chartrizard/ombi --values media.ombi.values.yml --namespace media
