# Benchmarks

TODO: Implement docker compose, meanwhile you can use this for building and running:

Client:
```sh
docker build -t metacall/metassr_benchmarks:client .
```

Next.js:
```sh
docker build -t nextjs-docker .
docker run -p 3000:3000 nextjs-docker
```
