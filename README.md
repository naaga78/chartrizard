# chartrizard
Helm repo

This repository contains Helm charts for various projects

* [Application 1](charts/app1/)
* [Sonarr](charts/sonarr/)
* [Radarr](charts/radarr/)
* [Lidarr](charts/lidarr/)
* [Jackett](charts/jackett/)
* [Transmission](charts/transmission-openvpn/)
* [Ubooquity](charts/ubooquity/)
* [Emby](charts/emby/)


## Installing Charts from this Repository

Add the Repository to Helm:

    helm repo add chartrizard https://naaga78.github.io/chartrizard/
    helm repo update

Install Application 1:

    helm install 'name' chartrizard/app1 

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

Install Emby:

    helm install emby chartrizard/emby --values media.emby.values.yml --namespace media