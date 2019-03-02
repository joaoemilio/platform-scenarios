# Micro Integrator - Demo Setup
Esse exemplo demonstra como utilizar o WSO2 Micro Integrator seguindo as instruções da documentação oficial do WSO2 Enterprise Integrator [EI Documentation](https://docs.wso2.com/display/EI640/Sending+a+Simple+Message+to+a+Service+Using+the+Micro+Integrator)

# Como Executar essa Demo?
   
## Instruções para Windows 10 Home 

1. Faça o Download e Instale o [docker-toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/)
```
## Caso tenha a distribuição Windows 10 Professional, utilize o suporte nativo para docker
```
2. Crie uma pasta c:\wso2 para baixar esse repositório. Isso vai ajudar a montar os volumes / mounts dos containers docker
> Por exemplo, ao executar esse comando no docker quickstart terminal, você conseguirá fazer o deploy de um microservice utilizando a imagem oficial WSO2 apontando para o diretório onde fizer o git clone
  ```bash
    docker run 
      -p 9090:9090 \
      --mount type=bind,source=/wso2/platform-scenarios/micro-integrator-sample/v1.0.0/msf4j-setup/resources/microservices,target=/home/wso2carbon/wso2ei-6.4.0/wso2/msf4j/deployment/microservices/ \
      docker.wso2.com/wso2ei-msf4j:6.4.0
  ```

3. Abra a GUI do Oracle Virtual Box e compartilhe com a Virtual Machine "default" a pasta criada acima
<img src="https://raw.githubusercontent.com/joaoemilio/platform-scenarios/master/micro-integrator-sample/images/oracle-virtual-box-shared-folder.jpg" height="50%" width="50%">

4. Abra o Docker QuickStart Terminal
> Repare que a primeira linha do terminal depois da baleia mostra o IP em que seus containers vão rodar.

<img src="https://raw.githubusercontent.com/joaoemilio/platform-scenarios/master/micro-integrator-sample/images/docker-quickstart-terminal.jpg" height="50%" width="50%">
