Here's how to run CoMotion on Docker:
1. According to the repository readme, get the SMPL model and rename it. Move it to `docker/app/SMPL_NEUTRAL.pkl` instead of the path given in the readme.
2. Move the input video or image(s) that you want to run CoMotion on to `docker/app/input/`.
3. In `docker/compose.yaml`, set the environment variable `INPUT_NAME` on line 7 to the file name of your input.
4. In `docker/compose/app/Dockerfile`, make sure the CMD command is to your liking. `INPUT_NAME` is defined by `docker/compose.yaml`, but you should vary the other flags and arguments to suit your input.
5. Navigate to `docker/app` and run `docker compose build` to build the image. If you also want to run CoMotion in a container after building the image, run `docker compose up --build`.
6. You can access the output of CoMotion wherever your Docker volumes are located (this depends on your file system)