# Ubooquity

Ubooquity is a free, lightweight and easy-to-use home server for your comics and ebooks. Use it to access your files from anywhere, with a tablet, an e-reader, a phone or a computer.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/ubooquity/
    sudo chmod -R 777 /mnt/ssd/media/configs/ubooquity

Values file example:

    replicaCount: 1

    image:
      repository: linuxserver/ubooquity
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

    volumeMounts:
      - name: media-ssd
        mountPath: "/config"
        subPath: "configs/ubooquity"
      - name: hdd-ssd
        mountPath: "/books"
        subPath: books
      - name: hdd-ssd
        mountPath: "/comics"
        subPath: comics
      

Install ubooquity:

    helm install ubooquity chartrizard/ubooquity --values media.ubooquity.values.yml --namespace media

Additionnal note:
   to access the admin page, go to the kubernetes dashboard, look for the ubooquity service and just change the port from 2202 to 2203
   then access the admin page by adding :
    .../admin
   to the url









