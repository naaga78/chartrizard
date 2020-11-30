# lidarr

Lidarr is a music collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new tracks from your favorite artists and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/lidarr/
    sudo chmod -R 777 /mnt/ssd/media/configs/lidarr

    sudo nano /mnt/ssd/media/configs/lidarr/config.xml

    <Config>
	...
      <UrlBase>/lidarr</UrlBase>
	...
    </Config>

Values file example:

    replicaCount: 1

    image:
      repository: linuxserver/lidarr
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
        subPath: "configs/lidarr" 
      - name: hdd-ext
        mountPath: "/downloads/transmission"
        subPath: "downloads/transmission"
      - name: hdd-ssd
        mountPath: "/Musique"
        subPath: Musique
      

Install lidarr:

    helm install lidarr chartrizard/lidarr --values media.lidarr.values.yml --namespace media











