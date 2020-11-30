# transmission-openvpn

This container contains OpenVPN and Transmission with a configuration where Transmission is running only when OpenVPN has an active tunnel. It has built in support for many popular VPN providers to make the setup easier.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/transmission-data
    sudo chmod -R 777 /mnt/ssd/media/configs/transmission-data

    kubectl create secret generic openvpn --from-literal username='user'  --from-literal password='password' --namespace media

Values file example:

    replicaCount: 1

    image:
      repository: "haugene/transmission-openvpn"
      tag: "latest-armhf" # Suffixed by -armhf to pull the ARM image
      pullPolicy: "IfNotPresent"

    env:
      - name: OPENVPN_PROVIDER
        value: "NORDVPN" # VPN provider. List of supported providers: https://haugene.github.io/docker-transmission-openvpn/supported-providers/
      - name: OPENVPN_USERNAME
        valueFrom: # Reference to the secret | openvpn.username
          secretKeyRef:
            name: "openvpn"
            key: "username"
      - name: OPENVPN_PASSWORD
        valueFrom: # Reference to the secret | openvpn.password
          secretKeyRef:
            name: "openvpn"
            key: "password"
      - name: NORDVPN_PROTOCOL
        value: "TCP"
      - name: NORDVPN_COUNTRY
        value: "CH" # Country where we want to download over VPN
      - name: NORDVPN_CATEGORY
        value: "P2P" # VPN Type
      - name: LOCAL_NETWORK
        value: "192.168.1.0/24"
      - name: TRANSMISSION_PEER_PORT
        value: "47444"
      - name: TRANSMISSION_DOWNLOAD_DIR
        value: "/downloads/transmission"
      - name: PUID
        value: "1000"
      - name: PGID
        value: "1000"

    service:
      type: ClusterIP
      port: 80

    volumes:
      - name: "media-ssd"
        persistentVolumeClaim:
          claimName: "media-ssd"

      - name: "hdd-ext"
        persistentVolumeClaim:
          claimName: "hdd-ext"

      - name: "dev-tun" # Needed for VPN
        hostPath:
          path: "/dev/net/tun"

    volumeMounts:
      - name: "media-ssd"
        mountPath: "/data"
        subPath: "configs/transmission-data" 
      - name: "hdd-ext"
        mountPath: "/downloads/transmission"
        subPath: "downloads/transmission" 
      - name: "dev-tun"
        mountPath: "/dev/net/tun" # Needed for VPN

    securityContext:
      capabilities: # Needed for VPN
        add:
          - NET_ADMIN
      

Install transmission:

    helm install transmission chartrizard/transmission-openvpn --values media.transmission-openvpn.values.yml --namespace media











