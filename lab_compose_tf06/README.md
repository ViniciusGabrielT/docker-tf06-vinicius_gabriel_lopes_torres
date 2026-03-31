# ``docker-compose up -d`` (mostrando a criação dos recursos):

````bash
vinicius@DESKTOP-IDHRFR8:~/aulas_lab/aula006/app/docker-tf06-vinicius_gabriel_lopes_torres/lab_compose_tf06$ docker-compose up -d
[+] Building 5.5s (7/7) FINISHED
 => [internal] load local bake definitions                                                                                                                                                                    0.0s
 => => reading from stdin 676B                                                                                                                                                                                0.0s
 => [internal] load build definition from Dockerfile                                                                                                                                                          0.1s
 => => transferring dockerfile: 64B                                                                                                                                                                           0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                                                                                                                                               1.3s
 => [internal] load .dockerignore                                                                                                                                                                             0.0s
 => => transferring context: 2B                                                                                                                                                                               0.0s
 => CACHED [1/1] FROM docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203cd34cf6d1                                                                                  0.1s
 => => resolve docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203cd34cf6d1                                                                                         0.1s
 => exporting to image                                                                                                                                                                                        0.5s
 => => exporting layers                                                                                                                                                                                       0.0s
 => => exporting manifest sha256:5cbf7638e5b50beb15e436e87ac983bb3b8c3ba39afd9016bb72d782f0d96d83                                                                                                             0.0s
 => => exporting config sha256:a9eae976029bca0532f5dc61f2cc4d8e43bebd2dc236629d81431ad0cb76ec8a                                                                                                               0.0s
 => => exporting attestation manifest sha256:8228f1763ec1f7b4928eeca00909630d1031a95c54de9ea0f8ec4cee2a2ea32c                                                                                                 0.1s
 => => exporting manifest list sha256:4285ac303f116433c31b0d4696961c87bbcfdac880b37b533a7b5958a7391ac8                                                                                                        0.0s
 => => naming to docker.io/library/lab_compose_tf06-web_app:latest                                                                                                                                            0.1s
 => => unpacking to docker.io/library/lab_compose_tf06-web_app:latest                                                                                                                                         0.0s
 => resolving provenance for metadata file                                                                                                                                                                    0.1s
[+] up 5/5
 ✔ Image lab_compose_tf06-web_app     Built                                                                                                                                                                   6.2s
 ✔ Network lab_compose_tf06_default   Created                                                                                                                                                                 0.4s
 ✔ Volume lab_compose_tf06_redis_data Created                                                                                                                                                                 0.0s
 ✔ Container compose-redis-tf6        Created                                                                                                                                                                 0.5s
 ✔ Container compose-web-tf6          Created
````

# ``docker-compose ps`` (mostrando os serviços ativos):

````bash
vinicius@DESKTOP-IDHRFR8:~/aulas_lab/aula006/app/docker-tf06-vinicius_gabriel_lopes_torres/lab_compose_tf06$ docker-compose ps
NAME                IMAGE                      COMMAND                  SERVICE    CREATED         STATUS         PORTS
compose-redis-tf6   redis:alpine               "docker-entrypoint.s…"   db_cache   3 minutes ago   Up 3 minutes   6379/tcp
compose-web-tf6     lab_compose_tf06-web_app   "/docker-entrypoint.…"   web_app    3 minutes ago   Up 3 minutes   0.0.0.0:8000->80/tcp, [::]:8000->80/tcp
````

# Um teste de conectividade (``ping``) entre os contêineres:

````bash
vinicius@DESKTOP-IDHRFR8:~/aulas_lab/aula006/app/docker-tf06-vinicius_gabriel_lopes_torres/lab_compose_tf06$ docker-compose exec web_app sh
/ # ping db_cache
PING db_cache (172.18.0.2): 56 data bytes
64 bytes from 172.18.0.2: seq=0 ttl=64 time=2.566 ms
64 bytes from 172.18.0.2: seq=1 ttl=64 time=0.267 ms
64 bytes from 172.18.0.2: seq=2 ttl=64 time=0.201 ms
64 bytes from 172.18.0.2: seq=3 ttl=64 time=0.180 ms
64 bytes from 172.18.0.2: seq=4 ttl=64 time=0.201 ms
^C
--- db_cache ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.180/0.683/2.566 ms
````