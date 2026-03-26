#  docker uses
with cloud services, it's no longer a production platform
it's a specialized tool for
1) dev
2) ci/cd
3) packaging

## for dev
industry standard, create local consistent env, match production cloud env
package code, libraries, config into single image
so do local dev, test, then only push to production cloud

## ci/cd
github actions uses docker to build, test, scan images before deploy
then ci/cd store image as artifact in cloud registry like amazon elastic container registry

## packaging and deployment
needed in cloud orchestration (kubernetes) for scaling
docker create the containers, kubernetes manage how they are deployed and scaled across cloud
but amazon ecs, aws fargate support docker containers, no need manage yourself