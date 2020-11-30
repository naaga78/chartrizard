# Jackett

Jackett works as a proxy server: it translates queries from apps (Sonarr, SickRage, CouchPotato, Mylar, etc) into tracker-site-specific http queries, parses the html response, then sends results back to the requesting software. This allows for getting recent uploads (like RSS) and performing searches. Jackett is a single repository of maintained indexer scraping & translation logic - removing the burden from other apps.

## Install and configuration

Personnal configuration example:

    sudo mkdir -p /mnt/ssd/media/configs/jackett/
    sudo chmod -R 777 /mnt/ssd/media/configs/jackett

    sudo nano /mnt/ssd/media/configs/jackett/config.xml

    <Config>
	...
      "BasePathOverride": "/jackett"
	...
    </Config>

Values file example:

    replicaCount: 1

    image:
      repository: "gjeanmart/jackettvpn" # Special image to use Jackett over a VPN
      tag: "arm-latest"
      pullPolicy: IfNotPresent

    env:
      - name: VPN_ENABLED
        value: "yes" 
      - name: VPN_USERNAME
        valueFrom:
          secretKeyRef: 
            name: "openvpn"
            key: "username"
      - name: VPN_PASSWORD
        valueFrom:
          secretKeyRef: 
            name: "openvpn"
            key: "password"
      - name: LAN_NETWORK
        value: "192.168.1.0/24"
      - name: CREATE_TUN_DEVICE
        value: "true" # Needed for VPN
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
      - name: "dev-tun"  
        hostPath:
          path: "/dev/net/tun"

    volumeMounts:
      - name: "media-ssd"
        mountPath: "/config"
        subPath: "configs/jackett" 

    securityContext:
      capabilities: 
        add:
          - NET_ADMIN
      

Install radarr:

    helm install jackett chartrizard/jackett --values media.jackett.values.yml --namespace media











