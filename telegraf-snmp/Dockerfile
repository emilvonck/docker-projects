FROM telegraf:1.21.4

# RUN sed -i -e "s/ main/ main contrib non-free/g" /etc/apt/sources.list \
#     &&  apt-get update && apt-get install -y --no-install-recommends \
#     snmp-mibs-downloader \
#     &&  rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends git && \
    rm -rf /var/lib/apt/lists/* \
    && git clone \
    --depth 1  \
    --filter=blob:none  \
    --sparse \
    https://github.com/librenms/librenms.git /usr/share/snmp/mibs/librenms \
    ; git -C /usr/share/snmp/mibs/librenms sparse-checkout set mibs

RUN sed -i "/mibs :/s/^/# /" /etc/snmp/snmp.conf \
    && sed -i "/mibdirs/s/^# //g" /etc/snmp/snmp.conf \
    && sed -i "/mibdirs/s/$/:\/usr\/share\/snmp\/mibs\/librenms\/mibs/" /etc/snmp/snmp.conf
