# NOT WORKING!


### Running HTTP workload generator

##### Template
```bash
cd <path-of-repo>/socialNetwork
./wrk -D exp -t <num-threads> -c <num-conns> -d <duration> -L -s ./wrk2/scripts/hotel-reservation/mixed-workload_type_1.lua http://<external-ip-address>:5000 -R <reqs-per-sec>
```

##### Example
```bash
sudo apt -y install luarocks
sudo luarocks install luasocket
git clone https://github.com/tgiannoukos/DeathStarBench.git
cd DeathStarBench/wrk2/
make all
cd ../mediaMicroservices/
helm install media helm-chart/mediamicroservices/

../wrk2/wrk -D exp -t 1 -c 1 -d 1 -L -s ./wrk2/scripts/media-microservices/compose-review.lua http://1.2.4.116:8080/wrk2-api/review/compose -R 10

```


### View Jaeger traces

Use `ssh -L 9090:1.2.4.115:16686 username@host` to connect to the host using ssh tunneling.

View Jaeger traces by accessing `http://localhost:9090/`


