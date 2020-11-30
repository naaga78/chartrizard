# Muximux

Muximux is a lightweight portal to view & manage your HTPC apps without having to run anything more than a PHP enabled webserver. With Muximux you don't need to keep multiple tabs open, or bookmark the URL to all of your apps.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/muximux/
    sudo chmod -R 777 /mnt/ssd/media/configs/muximux


Values file example:

    replicaCount: 1

    image:
      repository: linuxserver/muximux
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

    volumeMounts:
      - name: media-ssd
        mountPath: "/config"
        subPath: "configs/muximux" 
      

Install Muximux:

    helm install muximux chartrizard/muximux --values media.muximux.values.yml --namespace media











