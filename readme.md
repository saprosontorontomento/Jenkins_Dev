# Jenkins Developments

## JOBS

### JOB start stub
echo "---------------Build Started---------------" \
echo "---------------Build by Jenkins ID#  $BUILD_ID---------------" \
echo "---------------stub starts---------------" \
BUILD_ID=dontKillMe nohup java -javaagent:jolokia-jvm-1.7.1-agent.jar=port=8778,host=0.0.0.0 -jar mock11java.jar &

### JOB stop stub (kill PID)
ps aux | grep java | grep mock \
sudo kill $(ps aux | grep java | grep mock | awk '{print $2}')

### JOB start Dockerfile stub

sudo docker build -f /home/ubuntu/Рабочий\ стол/docker/Dockerfile -t stub . \
docker run -d -p 8008:8008 stub

### JOB stop Dockerfile stub

docker ps | grep stub | awk '{print $1}' | xargs docker stop

### JOB start docker-compose ---- start prometheus

cd /etc/prometheus \
docker-compose up -d

### JOB stop docker-compose ---- stop prometheus

cd /etc/prometheus \
docker-compose stop

### delete-docker-ps-and-image ---- stub

docker rm -v $(docker ps -aq -f status=exited) \
docker images -a | grep stub | awk '{print $3}' | xargs docker rmi

## commands

### Удаление контейнеров

docker rm -v $(docker ps -aq) # Все \
docker rm -v $(docker ps -q) # Все активные \
docker rm -v $(docker ps -aq -f status=exited) # Все неактивные \

### Удаляем "висячие образы"
docker rmi $(docker images -f "dangling=true" -q)

