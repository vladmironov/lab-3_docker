## Лабораторная работа №3 по Docker Redis

Представляю вашему вниманию лабораторную работу по запуску Redis и кнопочному приложению Rocket-counter

## Инструкция

**Важно!** Для запуска и проверки необходимы следующие компоненты:
- Dcoker + WSL 2
- Распакованная папка rocket-counter-main в любое удобное для вас место (поскольку официально образа Docker для rocketcounter не существует, он был создан вручную)

**1. Соберите образ из папки** 

```powershell
cd rocket-counter-main
docker build -t rocketcounter:latest .
```

На экране увидите примерно следующее
```powershell
[+] Building 140.7s (11/11) FINISHED                                                                                         docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 251B                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/python:alpine                                                                             2.4s
 => [auth] library/python:pull token for registry-1.docker.io                                                                                0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 2B                                                                                                              0.0s
 => [1/5] FROM docker.io/library/python:alpine@sha256:0f9552bb28711333da16915ec146f5e6bb44a7fdac9ced15dc17c2e0206346dd                       7.3s
 => => resolve docker.io/library/python:alpine@sha256:0f9552bb28711333da16915ec146f5e6bb44a7fdac9ced15dc17c2e0206346dd                       0.1s
 => => sha256:912101e0eb182d8de495d29926c22dd786b95952ff7d5c1a508aa3d534b8539b 247B / 247B                                                   0.3s
 => => sha256:55d6aff2002377528af40eb9c777124114ac87f34bc36b849eb998f9973d7360 15.40MB / 15.40MB                                             4.0s
 => => sha256:2d2b30fc2d843f381593f45cb2f3aa21b761f96fb7f3b2bf8c32028aa8e8785a 412.01kB / 412.01kB                                           1.4s
 => => sha256:881fc932939efef04ca120ad44bbd2c0917851eb247aa4995428afb1e80ede17 3.85MB / 3.85MB                                               4.6s
 => => extracting sha256:881fc932939efef04ca120ad44bbd2c0917851eb247aa4995428afb1e80ede17                                                    0.4s
 => => extracting sha256:2d2b30fc2d843f381593f45cb2f3aa21b761f96fb7f3b2bf8c32028aa8e8785a                                                    0.2s
 => => extracting sha256:55d6aff2002377528af40eb9c777124114ac87f34bc36b849eb998f9973d7360                                                    1.5s
 => => extracting sha256:912101e0eb182d8de495d29926c22dd786b95952ff7d5c1a508aa3d534b8539b                                                    0.0s
 => [internal] load build context                                                                                                            0.3s
 => => transferring context: 270.05kB                                                                                                        0.0s
 => [2/5] WORKDIR /code                                                                                                                      0.1s
 => [3/5] RUN apk add --no-cache gcc musl-dev linux-headers                                                                                104.8s
 => [4/5] COPY . .                                                                                                                           0.1s
 => [5/5] RUN pip install -r requirements.txt                                                                                                9.2s
 => exporting to image                                                                                                                      16.4s
 => => exporting layers                                                                                                                      7.7s
 => => exporting manifest sha256:e10baa2f68fdbbc9bb5bf2517c0365822c175ad81706db63669c714f22e04728                                            0.0s
 => => exporting config sha256:c1b4ad90947b53b9a876a6db52be274fdc643f2f56a5563294b523591f2760a7                                              0.0s
 => => exporting attestation manifest sha256:ed007496f48e2376c3cf019a6d869d1b9c85331ff4ee4f6b055322bbb2fafdab                                0.0s
 => => exporting manifest list sha256:013f207c08b7cf6cc69f6adce728cd3a0780c130f68c300c52f8a68aba3d2fcb                                       0.0s
 => => naming to docker.io/library/rocketcounter:latest                                                                                      0.0s
 => => unpacking to docker.io/library/rocketcounter:latest
```

**2. Запустите Redis**

```powershell
docker run -d --name redis redis
```

**3. Запускаем сначала на порту 8085:5000**

```powershell
docker run -d --name rocketcounter -p 8085:5000 --link redis:redis rocketcounter:latest
```

**и создаем копии после остановки**

```powershell
docker compose up -d --scale rocketcounter=2
```

**Приятного использования!**

