# AsciiArtify. Minimum Viable Product

> Configuring the application that will be automatically deployed in Kubernetes

1. In the ArgoCD panel click `+ NEW APP`
2. In the modal window that opens, fill in the fields:

   - **Applicaton Name:** desired name
   - **Project Name:** default
   - **AUTO-CREATE NAMESPACE:** ✓
   - **Repository URL:** a link to the repository containing the manifests for deployment
   - **Revision:** HEAD
   - **Path:** helm
   - **Cluster URL:** [https://kubernetes.default.svc](https://kubernetes.default.svc/)
   - **Namespace:** demo
3. Click `CREATE`

   As a result, the added application will be displayed on the panel:

   ![Screenshot-from-2023-11-28 18-26-43.png](../assets/Screenshot-from-2023-11-28_18-26-43.png)

4. Review the details of the application by clicking on the block **Demo.**

   ![Screenshot-from-2023-11-28 18-43-03.png](../assets/Screenshot-from-2023-11-28_18-43-03.png)

5. ArgoCD application has been created, but not yet deployed. Deploy it by performing the first synchronization by clicking the `Sync` button and selecting all components from the list in this case.

   ![Screenshot-from-2023-11-28 19-05-46.png](../assets//Screenshot-from-2023-11-28_19-05-46.png)

   The statuses will change to **Healthy**, **Syned**, **Sync OK**, this will mean that the project is fully deployed and the state of the source code matches the state in the repository.
6. As the state of the project in the repository changes, ArgoCD will notice the difference and report that the application is out of sync.

   Next, press the synchronization button again or set up automatic synchronization. Check this by editing the `helm/values.yaml` file in the repository, correcting the api-gateway type to `LoadBalancer`. Like this:

   ```bash
   api-gateway:
     image:
       tag: 0.51.2
     service:
       type: LoadBalancer
   ```
   Press `Refresh` button and see **OutOfSync** notification, ArgoCD tracked changes in the repository:

   ![Screenshot-from-2023-11-28 20-12-43.png](../assets/Screenshot-from-2023-11-28_20-12-43.png)

   If synchronize again, the state of the cluster will be updated according to the latest changes in the repository.
7. Test the application.

   - Return the `NodePort` value and make sure that everything is synchronized.
   - Set up port-forwarding for `ambassador`

     ```bash
     kubectl port-forward -n demo svc/ambassador 8082:80&
     ```
   - Check access

     ```bash
     curl localhost:8082
     ```
   - Upload image

     ```bash
     curl -F 'image=@img.jpg' localhost:8082/img/
     ```
     The app transforms the image into ASCII art

     Original:

     ![img.jpg](../assets/img.jpg)

     Result:

     ![Screenshot-from-2023-11-28 22-06-08.png](../assets/Screenshot-from-2023-11-28_22-06-08.png)

   Demo:

   [![asciicast](https://asciinema.org/a/wgiRhDrYWRGY0DlwWIdiUXJCF.svg)](https://asciinema.org/a/wgiRhDrYWRGY0DlwWIdiUXJCF)
