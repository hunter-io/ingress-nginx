# custom-error-pages

We use this image as the `default-backend-service` for the `kubernetes-ingress-controller`. We override the default `defaultbackend` image from Google (gcr.io/google_containers/defaultbackend) with this custom image to have custom error pages.

# How to update the image?

1. Move to `images/custom-error-pages`
2. Edit the HTML or JSON pages in `rootfs/www`
3. Build a new binary (don't forget to update the TAG)
```
TAG=0.8 REGISTRY=quay.io/hunter-io IMGNAME=nginx-backend make build
```
4. Build the new image (don't forget to update the TAG)
```
TAG=0.8 REGISTRY=quay.io/hunter-io IMGNAME=nginx-backend make all-container
```
5. Push that new image to the quay repository
```
docker push quay.io/hunter-io/nginx-backend:0.8
```
6. Then make the `nginx-backend` deployment use that new image
