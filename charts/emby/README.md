# Emby

Emby Server is a home media server built on top of other popular open source technologies such as Service Stack, jQuery, jQuery mobile, and .NET Core.
It features a REST-based API with built-in documention to facilitate client development. We also have client libraries for our API to enable rapid development.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/emby/


Values file example:

    replicaCount: 1

    image:
      repository: emby/embyserver
      tag: latest
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
        subPath: "configs/emby"
      - name: hdd-ssd
        mountPath: "/Films"
        subPath: Films
      - name: hdd-ssd
        mountPath: "/Films2"
        subPath: Films2
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
      

Install emby:

    helm install emby chartrizard/emby --values media.emby.values.yml --namespace media











