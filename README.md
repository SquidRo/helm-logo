## Usage

1. Clone the source
```shell
$ git clone  https://github.com/SquidRo/helm-logo
$ cd helm-logo
```

2. Put logo.svg and favicon.ico into logo directory

3. Use the helm to generate logo-sec.yaml 
```shell
$ helm template -s templates/logo-sec.yaml <name> -n <namespace> . > logo-sec.yaml
```

4. Create the secret
```shell
$ kubectl apply -f logo-sec.yaml
```

5. Edit the deployment to use the new logo, ex:
```shell
apiVersion: apps/v1
kind: Deployment
...
        volumeMounts:
        - mountPath: /opt/kubesphere/console/dist/assets/logo.svg
          name: sq-logo
          subPath: logo.svg
        - mountPath: /opt/kubesphere/console/dist/assets/favicon.ico
          name: sq-logo
          subPath: favicon.ico
...
      volumes:
      - name: sq-logo
        secret:
          defaultMode: 420
          secretName: sq-sec-logo
```

