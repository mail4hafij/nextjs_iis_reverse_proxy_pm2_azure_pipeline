# nextjs_iis_reverse_proxy_pm2_azure_pipeline
Deploy Nextjs App in windows IIS (reverse proxy) using pm2 node service through Azure devops pipeline.

### VM setup
1. A windows VM with IIS setup   - make sure to install URL Rewrite https://www.iis.net/downloads/microsoft/url-rewrite and Application Request Routing https://iis-umbraco.azurewebsites.net/downloads/microsoft/application-request-routing
2. Setup a reverse proxy rule in the ```URL Rewrite``` of a blank site to localhost:3000 (whatever port we want our nextjs/node application to run)
3. Install pm2 globally.

   ```npm install pm2 -g```
   
   Also need to add the following path to system environment path variable. So that our ```Deployment group job``` from azure release pipeline can run pm2 commands.
   
   ```C:\Users\{your_username}\AppData\Roaming\npm\node_modules\pm2\bin```
   ```C:\Users\{your_username}\.pm2```
   
5. Make sure to restart the VM.
6. Create a folder ```Next``` in the C: drive. This is where we will run our node or nextjs application.
   
### Azure Build and Release pipelines   
6. Follow the build pipeline from the repo https://github.com/mail4hafij/nextjs_azure_devops_pipeline
7. The build pipeline will create an artifact (let's say) which is ```next.zip```.
8. Create a deployment group which points to the windows VM in preperation for the release pipeline in azure.
9. In the release pipeline add two tasks 
    
   - ```Deployment group job``` - where we mention the deployment group which is the same as our iis server.
   
   - ```Command Line Script``` - use the following script. In the advance settings, make sure to be in the same directory where the artifact is downloaded.

```
call pm2 delete all
move /y .\next.zip C:\\Next
cd C:\\Next
tar -xvf next.zip
call pm2 start ecosystem.config.js 
```

Enjoy!
