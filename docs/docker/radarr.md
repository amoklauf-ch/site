# Radarr

## A mixed bag

This example has a lot of additional stuff. It shows you different ways to define something.

> :memo: All the variables ```${Something}``` are in an .env file. 

```yaml
  radarr:
    container_name: radarr
    image: ${RADARR}
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
      - DISCORD_WEBHOOK=${RADARR_DISCORD_WEBHOOK} # https://hotio.dev/arr-discord-notifier/
      - TMDB_API_KEY=${TMDB_API_KEY} # https://hotio.dev/arr-discord-notifier/
      - DROP_FIELDS=${DROP_FIELDS_RADARR} # https://hotio.dev/arr-discord-notifier/
      - TP_HOTIO=${TP_HOTIO} # https://theme-park.dev/
      - TP_THEME=${TP_THEME} # https://theme-park.dev/
    hostname: radarr
    logging:
      driver: json-file
      options: 
        max-file: "3"
        max-size: "10m"
    ports:
      - ${PORT_RADARR_7878}:7878/tcp
      - ${PORT_RADARR_9898}:9898/tcp
    restart: always
    tty: true
    depends_on:
      - authelia
      - nzbget
      - prowlarr
    volumes:
      - ${DOCKERCONFDIR}/radarr:/config:rw
      - ${DOCKERDATADIR}:/data:rw
      - ${DOCKERCONFDIR}/scripts/${STARTUP_RADARR}:/etc/cont-init.d/99-theme # https://theme-park.dev/
    labels:
      - "org.hotio.pullio.notify=${PULLIO_NOTIFY}" # https://hotio.dev/pullio/
      - "org.hotio.pullio.update=${PULLIO_UPDATE}" # https://hotio.dev/pullio/
      - "org.hotio.pullio.discord.webhook=${PULLIO_DISCORD_WEBHOOK}" # https://hotio.dev/pullio/
      - "org.hotio.pullio.author.avatar=${AVATAR_RADARR}" #https://hotio.dev/pullio/
      - "swag=enable" # https://mods.linuxserver.io/?mod=swag Swag Auto Proxy
      - "swag_url=radarr.*" # https://mods.linuxserver.io/?mod=swag Swag Auto Proxy
      - "swag_auth=authelia" # https://mods.linuxserver.io/?mod=swag Swag Auto Proxy
```