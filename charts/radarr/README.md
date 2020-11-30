# Radarr

Radarr is a movie collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new movies and will interface with clients and indexers to grab, sort, and rename them. It can also be configured to automatically upgrade the quality of existing files in the library when a better quality format becomes available.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/radarr/
    sudo chmod -R 777 /mnt/ssd/media/configs/radarr

    sudo nano /mnt/ssd/media/configs/radarr/config.xml

    <Config>
	...
      <UrlBase>/radarr</UrlBase>
	...
    </Config>

Values file example:

    replicaCount: 1

    image:
      repository: linuxserver/radarr
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
        subPath: "configs/radarr" 
      - name: hdd-ext
        mountPath: "/downloads/transmission"
        subPath: "downloads/transmission"
      - name: hdd-ssd
        mountPath: "/Films"
        subPath: Films
      - name: hdd-ssd
        mountPath: "/Films2"
        subPath: Films2
      

Install radarr:

    helm install radarr chartrizard/radarr --values media.radarr.values.yml --namespace media











