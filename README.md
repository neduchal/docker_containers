# uwb_ros2_docker


Příkaz na zobrazení GUI uvnitř kontejneru. Nutno provést na hostovském PC

> xhost +local:*

Pro využití GPU nutné nainstalovat balík nvidia-docker2

> distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
         && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
         && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
               sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
               sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

>sudo apt-get update

> sudo apt-get install -y nvidia-docker2

> sudo systemctl restart docker

Ukázkové spuštění se vším všudy

> docker run -i --privileged --name realsensetest --device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl -v /dev:/dev -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /home/neduchal/Dokumenty/Projekty/nck:/home/neduchal/nck --rm --gpus all  ros2test:latest /bin/bash 

> docker run -i --privileged --name uwb_ros2_test --device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl -v /dev:/dev -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /home/neduchal/Dokumenty/Projects:/home/neduchal/Projects --rm --gpus all  uwbros2docker:latest /bin/bash 

Spuštění pro testovací kontejnery home_navigation:

> docker run --privileged -d --name home_navigation_foxy --device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl -v /dev:/dev -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /home/neduchal/Dokumenty/Projects/ros2_custom_msgs:/home/neduchal/ros2_ws/src/ros2_custom_msgs -v /home/neduchal/Dokumenty/Projects/t265_ros2_wrapper:/home/neduchal/ros2_ws/src/t265_ros2_wrapper -w /home/neduchal/ros2_ws --rm --gpus all home_navigation_foxy:latest tail -f /dev/null

A pak dále připojení, které připojí prostředí ROSu:

>  docker exec --privileged -it home_navigation_foxy bash -c "source /ros_entrypoint.sh && bash"


> docker run -it --privileged --runtime nvidia --network host --name exon -e DISPLAY=$DISPLAY -v /home/spravce/exon_jetson:/home/exon/code --rm exon_scan:latest /bin/bash


Poznamka :https://github.com/Pyrestone/jetson-fan-ctl



