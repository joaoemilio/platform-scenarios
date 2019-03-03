# WSO2 Micro Integrator: Simple Proxy Service Demo
Esse exemplo demonstra como utilizar o WSO2 Micro Integrator seguindo as instruções da documentação oficial do WSO2 Enterprise Integrator [EI Documentation](https://docs.wso2.com/display/EI640/Sending+a+Simple+Message+to+a+Service+Using+the+Micro+Integrator)

## Como Executar essa Demo?
   
### Instruções para Windows 10 Home 
   > Caso tenha a distribuição Windows 10 Professional não utilize as instruções dessa seção. Siga os passos da seção: [Instruções para Windows 10 Professional](#instruções-para-windows-10-professional)

1. Faça o Download e Instale o [docker-toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/)


2. Crie uma pasta c:\wso2 para baixar esse repositório. Isso vai ajudar a montar os volumes / mounts dos containers docker
   > Por exemplo, ao executar esse comando no docker quickstart terminal, você conseguirá fazer o deploy de um microservice utilizando a imagem oficial WSO2 apontando para o diretório onde fizer o git clone
     ```bash
      docker run 
      -p 9090:9090 \
      --mount type=bind,source=/wso2/platform-scenarios/micro-integrator-sample/v1.0.0/msf4j-setup/resources/microservices,target=/home/wso2carbon/wso2ei-6.4.0/wso2/msf4j/deployment/microservices/ \
      docker.wso2.com/wso2ei-msf4j:6.4.0
     ```

3. Abra a GUI do Oracle Virtual Box e faça as seguintes configurações:

   3.1 - Compartilhe com a Virtual Machine "default" a pasta criada acima
   <img src="https://raw.githubusercontent.com/joaoemilio/platform-scenarios/master/micro-integrator-sample/images/oracle-virtual-box-shared-folder.jpg" height="50%" width="50%">

   3.2 - Nessa mesma VM, altere as configurações de Rede para apontar as portas 8290 e 9090 do seu computador para redirecionar para as portas que os containers vão abrir na VM
    <img src="https://raw.githubusercontent.com/joaoemilio/platform-scenarios/master/micro-integrator-sample/images/virtualbox-port-forwarding-1.jpg" height="50%" width="50%">

    <img src="https://raw.githubusercontent.com/joaoemilio/platform-scenarios/master/micro-integrator-sample/images/virtualbox-port-forwarding-2.jpg" height="50%" width="50%">

4. Abra o Docker QuickStart Terminal
   > Repare que a primeira linha do terminal, depois da baleia, mostra o IP em que seus containers vão rodar. Quando usamos Windows 10 Home, não podemos utilizar, por exemplo: http://localhost/meusite, pois o container host é uma máquina virtual Oracle Virtual Box ou Hyper-V com um IP específico. No passo #3 o que fizemos foi redirecionar os requests do localhost nas portas 8290 e 9090 para esse IP.

   <img src="https://raw.githubusercontent.com/joaoemilio/platform-scenarios/master/micro-integrator-sample/images/docker-quickstart-terminal.jpg" height="75%" width="75%">

5. Navegue até a pasta criada no passo #2 e clone o repositório
    > **Docker QuickStart Terminal**
    ```bash
    cd /c/wso2/
    git clone https://github.com/joaoemilio/platform-scenarios
    ```
6. Entre no diretório referente ao demo do WSO2 Micro Integrator
    > **Docker QuickStart Terminal**
    ```bash
    cd platform-scenarios/micro-integrator-sample
    ```
7. Abra o arquivo .env que está no diretório e altere a variável DIR para a pasta em que você está
    > Para saber o caminho completo, vá no Docker QuickStart Terminal e digite o comando:
    ```bash
    pwd
    ```
    
    > **ATENÇÃO** no Windows 10 Home o caminho não é o do seu laptop/desktop e sim o da máquina virtual, que mapeamos no passo #2. Se você usou o mesmo nome e caminho que foi sugerido, então deve ser: 
    /wso2/platform-scenarios/micro-integrator-sample e não precisa alterar o arquivo. Caso contrário, se escolheu outro caminho, então deve saber o nome do file system que mapeou. Altere a variável DIR com o valor apropriado.

    ```
    DIR=/wso2/platform-scenarios/micro-integrator-sample/resources
    ```

8. Inicie os containers utilizando o Docker QuickStart Terminal
    > **Docker QuickStart Terminal**
    ```powershell
    docker-compose up -d --force-recreate
    ```
7. Faça um teste chamando o microservice
    > **PowerShell** (No Terminal do Visual Studio Code ou abra o Windows PowerShell pelo menu iniciar)
    ```powershell
    Invoke-RestMethod -Headers @{"Content-Type" = "application/json"} http://192.168.99.100:9090/healthcare/surgery
    ```
    > **curl** (Docker QuickStart Terminal)
    ```bash
    curl http://192.168.99.100:9090/healthcare/surgery | python -m json.tool
    ```

8. Agora chame o Proxy Service no WSO2 Micro Integrator 
    > **PowerShell** (No Terminal do Visual Studio Code ou abra o Windows PowerShell pelo menu iniciar)
    ```powershell
    Invoke-RestMethod -Headers @{"Content-Type" = "application/json"} http://192.168.99.100:8290/healthcare/querydoctor/surgery
    ```
    > **curl** (Docker QuickStart Terminal)
    ```bash
    curl http://192.168.99.100:8290/healthcare/querydoctor/surgery | python -m json.tool
    ```

### Instruções para Mac ou Linux

### Instruções para Windows 10 Professional