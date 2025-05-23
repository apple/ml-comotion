# get a base image that comes with Python 3.10
FROM python:3.10 AS final

# get the repository from GitHub, then set working directory to the repository folder
WORKDIR .
RUN git clone https://github.com/apple/ml-comotion
WORKDIR ./ml-comotion

# install all dependencies
RUN pip install -e '.[all]'

# get pretrained checkpoint
RUN bash get_pretrained_models.sh

# install necessary libraries
RUN apt-get update && apt-get install -y \
	libgl1 \
	xvfb \
	ffmpeg \
	&& rm -rf /var/lib/apt/lists/*

# assuming you have downloaded the SMPL body model according to the repository readme and then renamed and moved it to docker/app, we move it into the image
COPY SMPL_NEUTRAL.pkl ./src/comotion_demo/data/smpl/SMPL_NEUTRAL.pkl

# copy the input into the image by file/directory name defined in compose.yaml
COPY input/$INPUT_NAME $INPUT_NAME

# finally, after building the image, run the following commands to run CoMotion using the input defined in compose.yaml by default; modify the command line arguments to your liking
CMD Xvfb :0 -screen 0 640x480x24 & export DISPLAY=:0.0 \
	&& python demo.py -i $INPUT_NAME -o output/ --frameskip 1
