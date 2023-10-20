# Hotel Reservations on Kubernetes

## Pre-requirements

- A running Kubernetes cluster is needed.
- Pre-requirements mentioned [here](https://github.com/delimitrou/DeathStarBench/blob/master/hotelReservation/README.md) should be met.

```bash
sudo apt -y install luarocks
sudo luarocks install luasocket
```

## Running the Hotel Reservation application

### Before you start

- Ensure that the necessary local images have been made.
  - `<path-of-repo>/hotelReservation/kubernetes/scripts/build-docker-images.sh`
  if you intend to change it, remember to change the username and image name in the build script and also all deployments as well.
### Deploy services

run `kubectl apply -Rf <path-of-repo>/hotelReservation/kubernetes/`
and wait for `kubectl get pods` to show all pods with status `Running`.


### Running HTTP workload generator

##### Template
```bash
cd <path-of-repo>/hotelReservation
./wrk -D exp -t <num-threads> -c <num-conns> -d <duration> -L -s ./wrk2/scripts/hotel-reservation/mixed-workload_type_1.lua http://<external-ip-address>:5000 -R <reqs-per-sec>
```

##### Example
```bash
sudo apt -y install luarocks
sudo luarocks install luasocket
git clone https://github.com/tgiannoukos/DeathStarBench.git
cd DeathStarBench
kubectl apply -Rf hotelReservation/kubernetes/
cd wrk2/
make all
cd ../hotelReservation/
../wrk2/wrk -D exp -t 2 -c 2 -d 30 -L -s ./wrk2/scripts/hotel-reservation/mixed-workload_type_1.lua http://1.2.4.114:5000 -R 2

```


### View Jaeger traces

Use `ssh -L 9090:1.2.4.115:16686 username@host` to connect to the host using ssh tunneling.

View Jaeger traces by accessing `http://localhost:9090/`