# Sonarr

Sonarr is a PVR for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new episodes of your favorite shows and will interface with clients and indexers to grab, sort, and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.


## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/sonarr/
    sudo chmod -R 777 /mnt/ssd/media/configs/sonarr

    sudo nano /mnt/ssd/media/configs/sonarr/config.xml

    <Config>
      <UrlBase>/sonarr</UrlBase>
    </Config>

Values file example:

    replicaCount: 1

    image:
      repository: linuxserver/sonarr
      tag: arm32v7-latest # ARM image
      pullPolicy: IfNotPresent

    env:
      - name: PUID
        value: "1000"
      - name: PGID
        value: "1000"

    service:
      type: ClusterIP
      port: 80

    volumes:
      - name: media-ssd
        persistentVolumeClaim:
          claimName: "media-ssd"
      - name: hdd-ssd
        persistentVolumeClaim:
          claimName: "hdd-ssd"
      - name: hdd-ext
        persistentVolumeClaim:
          claimName: "hdd-ext" 

    volumeMounts:
      - name: media-ssd
        mountPath: "/config"
        subPath: "configs/sonarr" 
      - name: hdd-ext
        mountPath: "/downloads/transmission"
        subPath: "downloads/transmission"
      - name: hdd-ssd
        mountPath: "/Series"
        subPath: Series
      - name: hdd-ssd
        mountPath: "/Series2"
        subPath: Series2
      - name: hdd-ssd
        mountPath: "/animes"
        subPath: animes
      - name: hdd-ssd
        mountPath: "/documentaires"
        subPath: documentaires
      - name: hdd-ssd
        mountPath: "/Mini-series"
        subPath: Mini-series
      

Install Sonarr:

    helm install sonarr chartrizard/sonarr --values media.sonarr.values.yml --namespace media











