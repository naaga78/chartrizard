# Ombi

Ombi allows you to host your own Plex Request and user management system. If you are sharing your Plex server with other users, allow them to request new content using an easy to manage interface! Manage all your requests for Movies and TV with ease, leave notes for the user and get notification when a user requests something. Allow your users to post issues against their requests so you know there is a problem with the audio etc. Even automatically send them weekly newsletters of new content that has been added to your Plex server!

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/ombi/
    sudo chmod -R 777 /mnt/ssd/media/configs/ombi


Values file example:

    replicaCount: 1

    image:
      repository: linuxserver/ombi
      tag: latest 
      pullPolicy: IfNotPresent

    env:
      - name: PUID
        value: "1000"
      - name: PGID
        value: "1000"
      - name: "TZ"
        value: "Europe/Paris"

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
        subPath: "configs/ombi" 

Install Ombi:

    helm install ombi chartrizard/ombi --values media.ombi.values.yml --namespace media











