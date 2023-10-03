# nextjs_iis_reverse_proxy_pm2_azure_pipeline
Deploy Nextjs App in windows IIS (reverse proxy) using pm2 node service through Azure devops pipeline.

Steps: 

1. A windows VM with IIS setup -
    - make sure to install URL Rewrite https://www.iis.net/downloads/microsoft/url-rewrite
    - setup a reverse proxy rule in the URL Rewrite to localhost:3000 (whatever port you want your nextjs/node application to run)
2. Install pm2 globally. Also need to add the following path to system environment path variable so that, deployment group from azure pipeline can run pm2 commands.
   ```C:\Users\{your_username}\AppData\Roaming\npm\node_modules\pm2\bin```
3. Make sure to restart the VM.
4. Now let's look at the azure deployment and release pipelines -
5. Follow the build pipeline from the repo https://github.com/mail4hafij/nextjs_azure_devops_pipeline/tree/master
   
TODO... need to add release pipeline
