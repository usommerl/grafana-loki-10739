# grafana-loki-10739

See grafana/loki#10739

```
> docker-compose up -d

✔ Network promtail-docker-service-discover-issue_default     Created  0.0s
✔ Container loki                                             Started  0.0s
✔ Container gluetun                                          Started  0.0s
✔ Container promtail                                         Started  0.0s
✔ Container service-that-requires-access-to-the-vpn          Started  0.0s


> docker ps --format "table {{.Names}}\t{{.ID}}"
NAMES                                             CONTAINER ID
service-that-requires-access-to-the-vpn           1ba54cad111f
gluetun                                           c0a955fab336
loki                                              0541f258f001
promtail                                          cb4293056d33

> docker logs promtail 2>&1 | grep -i "added docker target"
level=info ts=2023-09-28T14:06:13.076872826Z caller=target_group.go:128 msg="added Docker target" containerID=c0a955fab336fa71faf369d3ee1c277c2cb93d6d4241869fa255b4b48dd26ac1
level=info ts=2023-09-28T14:06:13.076918823Z caller=target_group.go:128 msg="added Docker target" containerID=0541f258f001574313b68530aad40e654ab34d7b8a0fca974508ce90e5b8f76f
level=info ts=2023-09-28T14:06:13.076939236Z caller=target_group.go:128 msg="added Docker target" containerID=cb4293056d33be5a975d902868e9af8b9b2500bf3ad95cdecbfff6c1e7aa6542

# Note that promtail does not discover the container with ID 1ba54cad111f ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
