# FoundryVTT_KubernetesTemplate
 This is a template for deploying Foundry VTT to kubernetes so that it uses a local file storage, ingress, secret for login credentials, as well as retain changes over time

Something not found in the template is adding a tls cert so you can take advantage of https. I recommend looking into 

 This creates a namespace named foundry-vtt where the components are deployed to. If you're using an nginx-ingress controller I recommend looking over [this guide](https://kubernetes.github.io/ingress-nginx/user-guide/tls/)

## Items that you will need to set:
- ***ingress.yaml***
    - the ```spec.hostname``` needs to be set to **the host name portion of the url** you want players to enter to reach your server (the part between 'http://' and '/')
- ***secret.yaml***
    - the ```data.foundry_username``` needs to be set to the base64 encoded **username** you use to sign into [foundry](https://foundryvtt.com/)
    - the ```data.foundry_password``` needs to be set to the base64 encoded **password** you use to sign into [foundry](https://foundryvtt.com/)
- ***pvol.yaml***
    - the ```spec.local.path``` needs to be set to the **file directory** that the foundry files will be located
    - the ```spec.nodeAffinity.nodeSelectorTerms[matchesExressions[values[]]]``` must be set to the name of the **kubernetes host name** you want foundry deployed to
