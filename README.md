# test-image-uploading-service

Lets assume that the service has typical use-case: a user goes to a web page, chooses some images, crop them and upload to the service; then the images are available in public.

I will implement that kind of service with layers below:

* **Front-end.** This layer can be *react-js* or *js native* page with functions to choose an image and interface for image cropping. It can be hosted on *AWS CloudFront* with *S3* since the code is static (html, css, js).
* **Back-end.** The layer for WEB API to interact with service.
  * **Load balancer.** This layer can be based on *docker swarm*, *k8s* or *AWS ECS*.
Docker container. The WEB API implementation can be made on any suitable technologies (*dotnet core*, *go*, *python*, *node.js*). In terms of my specialty and company's team specialty the *C# dotnet core* with *asp.net webapi* framework is preferable. On that layer the code will process the images for resizing (configured) and push that images to Storage layer.
  * **Storage.** The main function of this layer is only to store images and made them public. The preferable way to do that is use *AWS S3* (maybe behind *CloudFront*) because it's scalable, cheap and simple file storage. S3 bucket can be made public and process image distribution requests itself.

This system design does not cover logging and monitoring subsystems because they must be defined outside of this system.
